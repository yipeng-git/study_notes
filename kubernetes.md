# Demo

创建集群

```bash
minikube start [--node n] # macOS 用docker做驱动有问题！！
```

创建 deployment

```
kubectl create deployment python-foo --image=docker.io/yipengdocker/python-docker:latest
kubectl apply -f deployment.yaml
```

暴露 service 的5000端口

```
kubectl expose deployment python-foo --type=NodePort --port 5000
```

此时没有 loadbalancer，无法从外部访问 service，让 kubernetes 对本机端口进行转发

```
kubectl port-forward service/python-foo :5000
```

可以从 localhost 访问了

横向扩展pods

```
kubectl scale deployment python-foo --replicas=4
```



# Hello Minikube

How to run a sample app on Kubernetes using minikube

## Starting minikube

```bash
# start minikube vm
minikube start
# open minikube dashboard
minikube dashboard
# get minikube dashboard url
minikube dashboard --url
```

## Create a Deployment

A Kubernetes *Pod* is a group of one or more Containers, tied together for the purposes of administration and networking. Usually Pod has only one Container. A Kubernetes *Deployment* checks on the health of your Pod and restarts the Pod's Container if it terminates. Deployments are the recommended way to manage the creation and scaling of Pods.

```bash
# create deployment
kubectl create deployment hello-node --image=k8s.gcr.io/echoserver:1.4
# view all deployments
kubectl get deployments
# view all pods
kubectl get pods
# view cluster events
kubectl get events
# view the kubectl configuration
kubectl config view
```

## Create a Service

By default, the Pod is only accessible by its internal IP address within the Kubernetes cluster. To make the Container accessible from outside the Kubernetes virtual network, you have to expose the Pod ad a Kubernetes *Service*.

```bash
# expose the Pod to the public internet
kubectl expose deployment hello-node --type=LoadBalancer --port=8080
# view the service created
kubectl get services
# access the service
minikube service hello-node
```

## Enable addons

```bash
# list the currently supported addons
minikube addons list
# enable an addon
minikube addons enable <addon-name>
# view the Pod and Service created
kubectl get pod,svc -n kube-system
# disable an addon
minikube addons disable <addon-name>
```

## Clean up

```bash
# clean up the resources created in the cluster
kubectl delete service hello-node
kubectl delete deployment hello-node
# stop the minikube vm
minikube stop
```

# Kubernetes Basics

## Kubernetes Clusters

Kubernetes coordinates a highly available cluster of computers that are connected to work as a single unit. Kubernetes automates the distribution and scheduling of application containers across a cluster in a more efficient way.

A kubernetes cluster consists of two types of recourses:

-   The **Control Plane** coordinates the cluster
-   **Nodes** are the workers that run applications

The Control Plane is responsible for managing the cluster (such as scheduling applications, maintaining applications's desired state, scaling applications, and rolling out new updates).

A node is a VM or a physical computer that serves as a worker machine in a Kubernetes cluster.

The nodes communicate with the control plane using the **Kubernetes API**.

## Kubernetes Deployments

Once you have a running Kubernetes cluster, you can deploy your containerized application on top of it. To do so, you create a Kubernetes **Deployment** configuration. The Deployment instructs Kubernetes how to create and update instances of your application.

Once the application instances are created, a Kubernetes Deployment Controller continuously monitors those instances. If the Node hosting an instance goes down or is deleted, the Deployment controller replaces the instance with an instance on another Node in the cluster. **This provides a self-healing mechanism to address machine failure or maintenance**.

## Kubernetes Pods

A Pod is a Kubernetes abstraction that represents a group of one or more application containers (such as Docker), and some shared resources for those containers. Those resources include:

-   Shared storage, as Volumes
-   Networking, as a uniuqe cluster IP address
-   Information about how to run each container, such as the container image version or specific ports to use

A Pod models an application-specific "logical host" and can contain different application containers which are relatively tightly coupled. The containers in a Pod share an IP address and port space, are always co-located and co-scheduled, and run in a shared context on the same Node.

Pods are the atomic unit on the Kubernetes platform. When we create a Deployment on Kubernetes, that Deployment creates Pods with containers inside them (as opposed to creating containers directly). Each Pod is tied to the Node where it is scheduled, and remains there until termination (according to restart policy) or deletion. In case of a Node failure, identical Pods are scheduled on other available Nodes in the cluster.

## Nodes

A Pod always runs on a **Node**. A Node is a worker machine in Kubernetes and may be either a virtual or physical machine, depending on the cluster. Each Node is managed by the Master. A Node can have multiple pods, and the Kubernetes master automatically handles scheduling the pods across the Nodes in the cluster. The Maters's automatic scheduling takes into account the available resources on each Node.

Every Kubernetes Nodes runs at least:

-   Kubelet, a process responsible for communication between the Kubernetes Master and the Node; it manages the Pods and the containers running on a machine.
-   A container runtime (like Docker) responsible for pulling the container image from a registry, unpacking the container, and running the application.

## Troubleshooting with kubectl

```
kubectl get - list resources
kubectl describe - show detailed information about a resource
kubectl logs - print the logs from a container in a pod
kubectl exec - execute a command on a container in a pod
```

## Kubernetes Services

Kubernetes **Pods** are mortal. Pods in fact have a **lifecycle**. When a worker nodes dies, the Pods running on the Node are also lost. A ReplicaSet might then dynamically drive the cluster back to desired state via creation of new Pods to keep your application running. As another example, consider an image-processing backend with 3 replicas. Those replicas are exchangeable; the frontend system should not care about backend replicas or even if a Pod is lost and recreated. That said, each Pod in a Kubernetes cluster has a unique IP address, even Pods on the same Node, so there needs to be a way of automatically reconciling changes among Pods so that your applications continue to function.

A Service in Kubernetes is an abstraction which defines a logical set of Pods and policy by which to access them. Services enable a loose between dependent Pods. A service is defined using YAML (preferred) or JSON, like all Kubernetes objects. The set of Pods targeted by a Service is usually determined by a *LabelSelector*.

Although each Pod has a unique IP address, those IPs are not exposed outside the cluster without a Service. Services allow your application to receieve traffic. Services can be exposed in different ways by specifying a `type` in the ServiceSpec:

-   *ClusterIP* (default) - Exposes the service on an internal IP in the cluster. This type makes the Service only reachable from within the cluster.
-   *NodePort* - Exposes the Service on the same port of each selected Node in the cluster using NAT. Makes a Service accessible from outside the cluster using <NodeIP>:<NodePort>. Superset of ClusterIP.
-   *LoadBalancer* - Creates an external load balancer in the current cloud (if supported) and assigns a fixed, external IP to the service. Superset of NodePort.
-   *ExternalName* - Maps the Service to the contents of the `externalName` field (e.g. `foo.bar.example.com`), by returning a `CNAME` record with its value. No proxying of any kind is set up. This type requires v1.7 or higher of `kube-dns`, or CORNDNS version 0.0.8 or higher.
-   Additionally, notes that there are some use cases with Service that involve not defining `selector` in the spec. A Service created without `selector` will also not create the corresponding Endpoints object. This allow users to manually map a Service to specific endpoints. Another possibility why there may be no selector is you are strictly using `type: ExternalName`.

## Services and Labels

A Service routes traffic across a set of Pods. Services are the abstraction that allow pods to die and replicate in Kubernetes without impacting your application. Discovery and routing among dependent Pods (such as the frontend and backend components in a application) is handled by Kubernetes Services.

Services match a set of POds using **labels and selectors**, a grouping primitive that allows logical operation on objects in Kubernetes. Labels are key/value pairs attached to objects and can be used in any number of ways:

-   Designate objects for development, test, and production
-   Embed version tags
-   Classify an object using tags

Labels can be attached to objects at creation time or later on. They can be modified at any time.

## Scaling an application

The previous Deployment created only one Pod for running application. When traffic increases, we will need to scale the application to keep up with user demand.

**Scaling** is accomplished by changing the number of replicas in a Deployment.

Scaling out a Deployment will ensure new Pods are created and scheduled to Nodes with available resources. Scaling will increase the number of Pods to the new desired state. Kubernetes also supports **autoscaling** of Pods. Scaling to zero is also possible, and it will terminate all POds of the specified Deployment.

Running multiple instances of an application will require a way to distribute the traffic to all of them. Services have an integrated load-balancer that will distribute network traffic to all Pods of an exposed Deployment. Services will monitor continuously the running Pods using endpoints, to ensure the traffic is sent only to available Pods.

```
kubectl scale deployments/kubernetes-bootcamp --replicas=4
```

## Updating an application

Users expect applications to be available all the time and developers are expected to deploy new versions of them several times a day. In Kubernetes this is done with rolling updates. **Rolling updates** allow Deployments' update to take place with zero downtime by incrementally updating Pods instances with new ones. The new Pods will be scheduled on Nodes with available resources.

In the previous module we scaled our application to run multiple instances. This is a reuirement for performing updates without affecting application availability. By default, the maximum number of Pods that can be unavailable during the update and the maximum number of new Pods that can be created, is one. Both options can be configured to either numbers or percentages (of Pods). In Kubernetes, updates are versioned and any Deployment update can be reverted to a previous (stable) version.

Similar to application Scaling, if a Deployment is exposed publicly, the Service will load-balance the traffic only to available Pods during the update. An available Pod is an instance that is available to the users of the application.

Rolling updates allow the following actions:

-   Promote an application from one environment to another (via container image updates)
-   Rollback to previous versions
-   Continuous Integration and Continuous Delivery of applications with zero downtime

```bash
# rolling update, the only thing to do is set a new image
kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2
# confirm the update
kubectl rollout status deployments/kubernetes-bootcamp
# roll back to the last working version
kubectl rollout undo deployments/kubernetes-bootcamp
```

# Configuration

# Stateless Applications

123

456
