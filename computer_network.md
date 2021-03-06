# 1. Computer Networks and the Internet

## 1.1 What is the Internet?

-   Nuts-and-Bolts: The basic hardware and software components make up the internet.
-   Networking Infrastructure that provides services to distributed applications.

### 1.1.1 A Nuts-and-Bolts Description

-   All devices are **Host** or **End Systems**.
-   Connected by a network of **communication links** and **packet switches**.
-   **Transmission rate** of links are measured in **bits/seconds**.
-   Basic formatted data of transmission: **packets** = **header** + **payload**.
-   Two most prominent types of packet switches are **routers** and **link-layer switches** .
-   Switches forward packet toward their ultimate destinations.
-   The sequence of communication links and packet switches traversed by a packet is known as a **route** or **path** through the network.
-   **Internet Service Providers** (**ISPs**) includes residential ISPs (local cable company or telephone companies), corporate ISPs, university ISPs and etc, provide internet services.
-   End systems and packet switches run **protocols** that control the sening and receiving of info within the Integnet.
-   Two most important protocols: **Transmission Control Protocol** (**TCP**) and **Internet Protocol** (**IP**).
-   Principal protocols **TCP/IP**.

### 1.1.2 A Services Description

-   Internet: *an infrastructure that provides services to applications*
-   **Distributed applications**: involves mutiple end systems that exchanges data with others. (Email, web surfing, IM, map, streaming)
-   End systems attached to the Internet provide a **socket interface** that specifies how a to deliver data to a specific destination on another end system. (a set of rules that the sending program must follow to deliver)

### 1.1.3 What is a Protocol?

*A **protocol** defines the format and the order of messages exchanged between two or more communicatiing entites, as well as the actions taken on the transmission and/or receipt of a message or other event.*

## 1.2 The Network Edge

-   End systems are referred to as *hosts* because they host (run) application programs. **End Systms = Hosts**
-   Hosts can be divided into **clients** and **servers**.
-   Today, most of the servers reside in large **data centers**.

### 1.2.1 Access Networks

#### Home Access: DSL, Cable FTTH, Dial-Up, and Satellite

Two most common broadband residential access: **Digital Subscriber Line** (**DSL**) and cable. 

-   DLS:
    -   ISPs: local telephone company that provides wired local phone access. (telco)
    -   Customer's DSL modem using the existing telephone line (twisted-pair copper wire) to exchange data with a digital subscriber line access multiplexer (DSLAM) in the telco's local central office (CO).
-   Cable Internet access:
    -   Makes use of the cable television company's existing cable television infrastructure.
    -   ISPs: local television company.
    -   Requires special modems called cable modems.
    -   Packets are send through a shared broadcast medium.
-   Fiber to the home (FTTH):

#### Avvess in the Enterprise (and the Home): Ethernet and WiFi

-   Local area network (**LAN**) is used to connect an end system to the edge router.
-   **Ethernet** is the most prevalent access technology in corporate, university, and home networks.
-   **WiFi** uses IEEE 802.11 standards.

#### Wide-Area Wireless Access: 3G and LTE

-   **LTE **= Long-Term Ebolution. It is actually not 4G, a miss used concept by the ISPs.

### 1.2.2 Physical Media

-   Propagating electromagnetic waves or optical pulses across a Physical medium.
-   Guided media (cables, wires) and unguided media (atmosphere).
-   The cost of the physical links (wires, cables) is often relatively minor compared with other networking costs.

#### Twisted-Pair Copper Wire

-   **Unshielded twisted pair (UTP)** is commonly used for computer networks within a building, for LAN.

#### Coaxial Cable

-   **Shared medium**, TV signal for example.

#### Fiber Optics

#### Terrestrial Radio Channels

-   Wireless LAN, cellular.

#### Satellite Radio Channels

-   **Geostationary satellites** (280 ms delay) and **low-earth orbiting (LEO) satellites** (Starlinks).

## 1.3 The Network Core

### 1.3.1 Packet Switching

End systems exchange **messages** with each other. Long messages are broke into smaller chunks of data known as **packets**. Packet travels through communication links and **packet switches**.

#### Store-andForward Transmission

-   Most packet switches must receive the entire packet before it can begin to transmit the first bit of the packet onto the outbound link.
-   End-to-end delay = #links * L/R, with (#links - 1) routers.

#### Queuing Delays and Packet Loss

-   Packet switch has an **out buffer**/**queue** for each attached link, which stores packets that is about to send into that link.
-   If an arriving packet needs to be transmitted onto a link but finds the link busy with transmission of another packet, the arrving packet mast wait, this causes **queuing delays**.
-   When the buffer is completely full, either the arriving packet or one of the already-queued packet will be droped. This is called **packet loss**.

#### Forwarding Tables and Routing Protocols

-   Each router has a **forwarding table** that maps destination address to that router's outbound links.
-   Forwarding tables are set automatically by **routing protocols**.

### 1.3.2 Circuit Switching

There are two fundamental switches: **circuit switching** and **packet switching**. The sender and the receiver must establish a connection, and the network must reserve one circuit on each of the links. The switches on the path between the sender and receiver maintain connection state for circuit connection. Transmission rate is a guaranteed constant rate. This is a dedicated end-to-end connection between the two hosts. 

#### Multiplexing in Circuit-Switched Networks

-   A circuit in a link is implemented with either **frequency-division multiplexing (FDM)** or ** time-division multiplexing (TDM)**.
-   FDM divides the frequency spectrum of a link. Telephone networks usually use 4 kHz, which is called **bandwidth**.

#### Packet Switching vs Circuit Switching

### 1.3.3 A Network of Networks

Connects ISPs. Evoloved into a very complex structure. Much of this evolution is driven by economics and national policy.

-   Network Structure 1 - interconnects all of the access ISPs with a *single global transit ISP*.
-   Network Structure 2 - consists of the hundreds of thousands of access ISPs and *multiple* global transit ISPs.
-   Network Structure 3 - multi-tier hierarchy.
-   Network Structure 4 - consists of access ISPs, regional ISPs, tier-1 ISPs, PoPs, multi-homing, peering, and IXPs.
    -   **Point of Presence (PoP)** - a group of one or more routers (at the same location) in the provider's network where customer ISPs can connect into the provider ISP.
    -   **Multi-home** - an ISP connect to two or more provider ISPs.
    -   **Peer** - a pair of nearby ISPs at the same level of the hierarchy directly connect their networks together so that all the traffic between them passes over the direct connection rather than through upstream intermediaries.
    -   **Internet Exchange Point (IXP)** - a meeting point where mutiple ISPs can peer together.
-   Network Structure 5 - builds on top of Network Structure 4 by adding content-provider networks.
    -   Content-providers build their own network and connect to lower-tier ISPs to bypass tier-1 ISPs.

## 1.4 Delay, Loss and Throughput in Packet-Switched Networks

Limited by physical laws.

### 1.4.1 Over view of Delay in Packet-Switched Networks

The most important of these delays are the **nodal processing delay, queuing delay, transmission delay**, and **propagation delay**; together, these delays accumulate to give a **total nodal delay**.

#### Types of Delay

-   **Processing Delay** - the time required to examing the packet's header and determine where to direct the packet.
-   **Queuing Delay** - the time packet waits to be transmitted onto the link.
-   **Transmission Delay** - the amount of time required to push all of the packet's bits into the link.
-   **Propagation Delay** - the time required to propagate from the beginning of the link to the end of the link.

#### Comparing Transmisison and Propagation Delay

-   Depends on distance and link media.

### 1.4.2 Queuing delay and Packet Loss

-   **Trafic intensity** - (average rate at which bits arrive at the queue) / (transmission rate).
    -   La/R > 1, arriving rate exceeds transmission rate.
    -   Not usually sufficient to fully charaterize the queuing delay statistics.

#### Packet Loss

When a packet arrives to find a full queue. With no place to store such a packet, a router will **drop** that packet; that is the packet will be **lost**.

### 1.4.3 End-to-End Delay

Suppose there are N-1 routers between the source host and the destination host.

-   End-to-end delay = N * (dproc + dtrans + dprop)

#### Traceroute

Suppose there are N-1 routers. Then the source will send N special packets into the network towards the ultimate destination. When the nth router receives the Nth packet, the router does not forward the packet but returns a message back to the source including the name and address of the router. In this manner, the source can reconstruct the route taken by packets flowing from source to destination and can determine the rount-trip delays to all internet routers. Traceroute repeats the experiment three times.

#### End System, Application, and Other Delays

-   An end system may *Purposefully* delay its transmission as part of protocol for sharing the medium with other end systems.
-   Media packetization delay such as Voice-over-IP (VoIP). The sending side must first fill a packet with encoded digitized speech before passing the packet to the Internet.

### 1.4.4 Throughput in Computer Networks

-   **Instantaneous throughput** - at any instant time.
-   **Average throughput** - time averaged.
-   Depends on the transmission rage of the **bottleneck link**.

## 1.5 Protocol Layers and Their Service Models

Internet is an *extremely* complicated system.

### 1.5.1 Layered Architecture

Each layer provides its service by:

-   Performing certain actions within that layer.
-   Using the services of the layer directly below it.

These layers are actually layers of **abstructions**!

#### Protocol Layering

-   Network designers organize protocols in **layers**.
-   Each layer has its **service model**.
-   Application-layer protocols are almost always implemented in software.
-   The physical layer and data link layers are typically implemented in hardware.
-   The network layer is often a mixed implementation of hardware and software.

The Internet protocol stack consists of five layers: the physical, link, network, transport, and application layers.

#### Application Layer

Includes many protocols, such as the HTTP protocol (provides for Web document request and transfer), SMTP (which provides for the transfer of e-mail messages), and FTP (which provides for the transfer of files between two end systems), DNS.

An application-layer protocol is distributed over multiple end system, which the application in one end system using the protocol to exchange packets of information with the application in another end system. We'll refer to this packet of information at the application layer as a message.

#### Transport Layer

The Internet's transport layer transports application-layer message between application endpoints. In the Internet there are two transport protocols, TCP and UDP, either of which can transportation application-layer messages. TCP provides a connection-oriented service to its applications. This service includes guaranteed delivery of application-layer messages to the destination and flow controls (that is, sender/receiver speed matching). TCP also breaks long message into shorter segments and provides a congestion-control mechanism, so that a source throttles its transmission rate when the network is congested. The UDP protocol provides a connectionless service to its applications. This is a no-frills service that provides no reliability, no flow control, and no congestion control. In this book, we'll refer to a transport-layer packet as a **segment**.

#### Network Layer

The Internet's network layer is responsible for moving network-layer packets known as **datagram** from one host to another. The Internet transport-layer protocol in a source host passes a transport-layer segment and a destination address to the network layer.

The Internet's network layer includes the celebrated IP protocol, which defines the fields in the datagram as well as how the end systems and routers act on these fields. There is only one IP protocol, and all Internet components that have a network layer must run the IP protocol. The Internet's network layer also contains routing protocols that determine the routes that datagrams take between sources and destinations. The Internet has many routing protocols.

#### Link Layer

To move a packet from one node to the next node in the route, the network layer relies on the services of the link layer. In particular, at each node, the network layer passes the datagram down to the link layer, which delivers the datagram to the next node along the route. At this next node, the link layer passes the datagram up to the network layer.

The services provided by the link layer depend on the specific link-layer protocol that is employed over thel ink. Examples of link-layer protocols include Ethernet, WiFi, and the cable access network's DOCSIS protocol. The link-layer packets are refered as **frames**.

#### Physical Layer

While the job of the link layer is to move entire frames from one network element to an adjacent network element, the job of the physical layer is to move the *individual bits* within the frame from one node to the next. The protocols in this layer are again link dependent and further depend on the actual transmission medium of the link (twisted-pair copper wire, single-mode fiber optics). Ethernet has manyh physical-layer protocols: one for twisted-pair copper wire, another for xoaxial cable, another for fiber, and so on. In each case, a bit is moved across the link in a different way.

#### The OSI Model

In the late 1970s, the International Organization for Standardization (ISO) proposed that computer networks be organized around seven layers, called the Open System Interconnection (OSI) model.

#### Presentation Layer and Session Layer

The role of the presentation layer is to provide services that allow communication applications to interpret the meaning of data exchanged. These services include data compression and data encryption as well as data description

The session layer provides for delimiting and synchronization of data exchange, including the means to build a checkpoint and recovery scheme.

It is up to the application developer to decide if a service is important, and if the service *is* important, it's up to the application developer to build that functionality into the application.

### 1.5.3 Encapsulation

At the sending host, an **application-layer message** is passed to the transport layer. In the simplest case, the transport layer takes the message and appends additional information (transport-layer header information) that will be used by the receiver-side transport layer. The application-layer message and the transport-layer header information together constitute the **transport-layer segment**. The transport-layer segment thus encapsulates the application-layer message . The added information might include information allowing the receiver-side transport layer to deliver the message up to the appropriate application, and error-detection bits that allow the receiver to determine whether bits in the message have been changed in route. The transport layer then passes the segment to the network layer, which adds network-layer header information such as source and destination end system addresses, creating a **network-layer datagram**. The datagram is then passed to the link layer, which will add its own link-layer header information and creat a **link-layer frame**. Thus we see that at each layer, a packet has two types of fields: header fields and a **payload field**. The payload is typically a packet from the layer above.

The actual process of encapsulation can be more complex than that described above.

## 1.6 Networks Under Attack

### 1.6.1 The Bad Guys Can Put Malware into Your Host Via the Internet

-   Malware
    -   Self-replicating
    -   Viruses
        -   Requires some form of user interaction to infect the user's device.
    -   Worms
        -   Can enter a device without any explicit user interaction.
-   Botnet

### 1.6.2 The Bad Guys Can Attack Servers and Network Infrastructure

-   Denial-of-service (DoS) attack
    -   *Vulnerability attack* - This incolves sending a few well-crafted messages to a vulnerable application or operating system running on a targeted host. If the right sequence of packets is sent to a vulnerable application or operating system, the service can stop or, worse, the host can crash.
    -   *Bandwidth flooding* - The attacker sends a deluge of packets to the targeted host - so many packets that the target's access link becomes clogged, preventing legitimate packets from reaching the server.
    -   *Connection flooding* - The attacker establishes a large number of half-open or fully open TCP connections at the target host. The host can becommes so bogged down with these bogus connections that it stops accepting legitimate connections.
-   Distributed DoS (DDoS)

### 1.6.3 The Bad Guys Can Sniff Packets

-   Packet sniffer

### 1.6.4The Bad Guys Can Masuerade as Someone You Trust

-   IP spoffing

## 1.7 History of Computer Networking and the Internet

### 1.7.1 The Development of Packet Switching: 1961-1972

### 1.7.2 Proprietary Networks and Internetworking: 1972-1980

###  1.7.3 A Proliferation of Networks: 1980-1990

### 1.7.4 The Internet Explosion: The 1990s

### 1.7.5 The New Millennium

# 2. Application Layer

## 2.1 Principles of Network

Network applications run in user's host.

### 2.1.1 Network Application Architechtures

An application's architechture is different from the network architechture. The **application architechture** is designed by the application developer and dictates how the application is structured over the various end systems. Two predominant architectural paradigms used in modern network applications: the client-server architechture or the peer-to-peer (P2P) architecture.

In a **client-server architecture**, there is always-on host, called the *server*, whichservices requests from many other hosts, called *clients*. A classic example is the Web application for which an always-on Web server services requests from browsers running on client hosts. Note that with the client-server architecture, clients do not directly communicate with each other. Another characteristic of the client-server architecture is that the server has a fixed, well-known address, called an IP address. Some of the better-known applications with a client-server architecture include the Web, FTP, Telnet, and e-mail.

Often in a client-server application, a single-server host is incapable of keeping up with all the requests from clients. For this reason, a **data center**, housing a large number of hosts, is often used to create a powerful virtual server. The most popular Internet services employ one or more data centers.

In a **P2P architechture**, there is minimal (or no) reliance on dedicated servers in data centers. Instead the application exploits direct communication between pairs of intermittently connected hosts, called *peers*. The peers are not owned by the service provider, but are instead desktops and laptops controlled by users. Many of today's most popular and traffic-intensive applications are based on P2P architectures. These applications include file sharing, peer-assisted download acceleration, and Internet telephony and video conference.

The most compelling features of P2P architechtures is their **self-scalability**.

### 2.1.2 Processes Communicating

In the jargon of operating system, it is not actually programs but **processes** that communicate. A processes can be thought of as a program that is running within an end system. When processes are running on the same end system, they can communicate with each other with interprocess communication, using rules that are governed by the end system's operating system. But in this book we are interested in how processes running on *different* hosts communicate.

Processes on two different end system communicate with each other by exchanging **messages** across the computer network.

#### Client and Server Processes

For each pair of communicating processes, we typically lable one of the two processes as the **client** and the other process as the **server**.

In some applications, such as in P2P file sharing, a process can be both a client and a server. We define the client and server processes as follows

*In the context of a communication session between a pair of processes, the process that initiates the communication (that is, initially contact the other process at the beginning of the session) is labeled as the* client. *The process that waits to be conntacted to begin the session is the server*.

#### The Interface Between the Process and the Computer Network

A process sends messages into, and receives messages from, the network through a software interface called a **socket**. 

A socket is the interface between the application layer and the transport layer within a host. It is also referred to as the **Application Programming Interface** (**API**) between the application and the network, since the socket is the programming interface with which network applications are built. The application developer has control of everything on the application-layer side of the socket but has little control of the transport-layer side of the socket. The only control that the application developer has on the transport-layer side is (1) the choice of transport protocol and (2) perhaps the ability to fix a few transport-layer parameters such as maximum buffer and maximum segment size. Once the application developer chooses a transport protocol, the application is built using the transport-layer services provided by that protocol.

#### Addressing Processes

In order for a process running on one host to send packets too a process running on another hosts, the receiving process needs to have an address. To identify the receiving process, two pieces of information need to be specified: (1) the address of the host and (2) an identifier that specifies the receiving processi n the destination host.

In the Internet, the host is identified by its **IP address**. It is a 32-bit unique identifier. In addition to knowing the address of the host to which a message is destined, the sending process must also identify the receiving process (more specifically, the receiving socket) running in the host. A destination **port number** serves this purpose. Popular applications have been assgned specific port numbers.

### 2.1.3 Transport Services Available to Applications

The application at the sending side pushes messages throught the socket. At the end side of the socket, the transport-layer protocol has the responsibility of getting the messages to the socket of the receiving process.

Many networks, including the Internet, provide more than one transport-layer protocol. When develop an application, you must choose one of the available transport-layer protocols. We can broadly classify the possible services along four dimensions: reliable data transfer, throughput, timing, and security.

#### Reliable Data Transfer

If a protocol provides a guaranteed data delivery service, it is said to provide **reliable data transfer**. One important service that a transport-layer protocol can potentially provide to an application is process-to-process reliable data transfer. When a transport protocol provides this service, the sending process can just pass its data into the socket and know with complete confidence that the data will arrive without errors at the receiving process.

When a transport-layer protocol doesn't provide reliable data transfer, some of the data sent by the sending process may never arrive at the receiving process. This may be acceptable for **loss-tolerant applications**, most notably multimedia applications such as conversational audio/vedio that can tolerate some amount of data loss. Lost data might result in a small glitch, but not a crucial impairment.

#### Throughput

A transport-layer protocol could provide guaranteed abailable throughput at some specified rate. Applications that have throughput requirements are said to be **bandwidth-sensitive applications**. Many current multimedia applications are bandwidth sensitive, although many of them may use adaptive coding techniques to encode digitized voice or video at a rate that matches the currently available throughput.

**Elastic applications** can make use of as much, or as little, throughput as happens to be available. E-mail, file transfer, and Web transfers are all elastic applications.

#### Timing

A transport-layer protocol can also provide timing guarantees. As with throughput guarantees, timing guarantees can come in many shape and forms. Such a service would be appealing to interactive real-time applications, such as Internet telephony, virtual environments, teleconferencing, and multiplayer games, all of which require tight timming constraints on data delivery in order to be effective. For non-real-time applications, lower delay is always preferable to higher delay, but no tight constraint is placed on the end-to-end delays.

#### Security

Finally, a transport protocol can provide an application with one or more security sevices. Such a service would provide confidentiality between the two processes, even if the data is somehow observed between sending and receiving processes. A transport protocol can also provide other security services in additional to confidentiality, including data integrity and end-point authentication.

### 2.1.4 Transport Services Provided by the Internet

The Internet (and, more generally, TCP/IP networks) makes two transport protocols available to applications, UDP and TCP.

#### TCP Services

The TCP service model includes a connection-oriented service and a reliable data transfer service. When an application invokes TCP as its transport protocol, the application receives both of these services from TCP.

-   *Connection-oriented service*. TCP has the client and server exchange transport layer control information with each other *before* the application-level message begin to flow. This is so-called handshaking procedure alerts the client and server, allowing them to prepare for an onslaught of packets. After the handshaking phase, a **TCP connection** is said to exist between the sockets of the two processes. The connection is a **full-duplex** connection in that the two processes can send messages to each other over the connection at the same time. When the application finishes sending messages, it must tear down the connection.
-   *Reliable data transfer service*. The communicating processes can rely on TCP to deliver all data sent without error and in the proper order. When one side of the application passes a stream of bytes into a socket, it can count on TCP to deliver the same stream of bytes to the receiving socket, with no missing or duplicate bytes.

TCP also includes a congestion-control mechanism, a service for the general welfare of the Internet rather than for the direct benefit of the communicating processes. The TCP congestion-control mechanism throttles a sending process (client or server) when the network is congested between sender and receiver. TCP congestion control also attempts to limit each TCP connection to its fair share of network bandwidth.

#### UDP Service

UDP is a no-frills, lightweight transport protocol, provoding minimal services. UDP is connectionless, so there is no handshaking before the two processes start to communicate. UDP procides an unreliable data transfer service--that is, when a process sends a message into a UDP socket, UDP provides *no* guarantee that the message will ever reach the receiving process. Futhermore, messages that do arrive at the receiving process may arrive out of order.

UDP does not include a congestion-control mechanism, so the sending side of UDP can pump data into the layer below (the network layer) at any rate it pleases.

#### Services Not Provided by Internet Transport Protocols

Today's Internet can often provide satisfactory service to time-sensitive applications, but it cannot provide any timming or throughput guarantees.

E-mail, remote terminal access, the Web, and file transfer all use TCP. These applications have chosen TCP primarily because TCP provides reliable data transfer, guaranteeing that all data will eventually get to its destination. Because Internet telephony applications can often tolerate some loss but require a minimal rate to be effective, developers of Internet telephony applications usually prefer to run their applications over UDP, thereby circumventing TCP's congestion control mechanism and packet overheads. But because many firewall are configured to block (most types of) UDP traffic, Internet telephony applications often are designed to use TCP as a backup if UCP communication fails.

### 2.1.5 Application-Layer Protocols

An application-layer protocol defines how an application's processes, running on different end systems, pass messages to each other. In particular, an application-layer protocol defines:

-   The types of messages exchanged, for example, request messages and response message.
-   The syntax of the various message types, such as the field in the message and how the fields are delineated.
-   The semantics of the fields, that is, the meaning of the information in the fields.
-   Rules for determining when and how a process sends messages and responds to messages.

Some application-layer protocols are specified in RFCs and are therefore in the public domain. For example, the Web's application-layer protocol, HTTP (the HyperText Transfer Protocol), is available as an RFC. If a browser developer follows the rules of the HTTP RFC, the browser will be able to retrieve Web pages from any Web serve that has also followed the rules of the HTTP RFC. Many other application-layer protocols are proprietary and intentionally not avaliable in the public domain. For example, Skype uses proprietary application-layer protocols.

Distinguish between network applications and application-layer protocols:

-   An application-layer protocols is only one piece of a network application.
-   A Web application consists of many components, including
    -   A standard for document formats (HTML)
    -   Web browsers
    -   Web servers
    -   Application-layer protocol.

The Web's application-layer protocol, HTTP defines the format and sequence of messages exchanged between browser and Web server. Thus HTTP is only one piece of the Web application.

### 2.1.6 Network Applications Covered in This Book

In this chapter we discuss five important applications: the Web, e-mail, directory service video streaming, and P2P applications.

## 2.2 The Web and HTTP

In the early 1990s, a major new application arrived on the scene--the World Wide Web. The Web was the first Internet application that caught the general public's eye. It dramatically changed, and continues to change, how people interact inside and outside their work environments. It elevated the Internet from jsut one of many data nwtworks to essentially the one and only data network.

Web operates *on demand*. Users receive what they want, when they want it. It is enormously easy for any individual to make information available over the Web--everyone can become a publisher at extremely low cost.

### 2.2.1 Overview of HTTP

The **HyperText Transfer Protocol** (**HTTP**), the Web's application-layer protocol, is at the heart of the Web. It is defined in [RCF 1945] and [RCF 2016]. HTTP is implemented in two programs: a client program and a server program. The client program and server program, executing on different end systems, talk to each other by exchanging HTTP messages. HTTP defines the structure of these messages and how the client and the server exchanged the messages.

Some Web terminology: A **Web page** (also called a document) consists of objects. An **object** is simply a file--such as an HTML file, a JPEG image, a Java applet, or a video clip--that is addressable by a single URL. Most Web pages consist of a **base HTML file** and several referenced objects. The base HTML file references the other objects in the page with the objects' URLs. Each URL has two components: the hostname of the server that houses the object and the object's path name. Because **Web browsers** implement the client side of HTTP, the context of the Web, will use the words*browser* and *client* interchangeably. **Web server**, which implement the server side of HTTP, house Web objects, each addressable by a URL. Popular Web servers include Apache and Microsoft Internet Information Server.

HTTP defines how Web clients request Web pages from Web servers and how servers transfer Web pages to client. When a user requests a Web page, the server receives the requests and responds with HTTP response messages that contain the object.

HTTP use TCP as its underlying transport protocol. The HTTP client first initiates a TCP connection with the server. Once the connection is estiblished, the browser and the server processes access TCP through their socket interfaces. TCP provides a reliable data transfer service to HTTP. Here is one of the great adventages of a layered architecture--HTTP need not worry about lost data or the details of how TCP recovers from loss or reordering of data within the network. That is the job of TCP and the protocols in the lower layers of the protocol stack.

The server sends requested files to clients without storing any state information about the client. Because an HTTP server maintains no information about the clients, HTTP is said to be a **stateless protocol**. The Web uses the client-server application architecture. A Web server is always on, with a fixed IP address, and it services requests from potentially millions of different browsers.

### 2.2.2 Non-Presistent and Presistent Connections

Depending on the application and how the application is being used, the series of requests may be made back-to-back, periodically at regular intervals, or intermittently. When this client-server interaction is taking place over TCP, the application developer needs to make an important decision--should each request/response pair be sent over a *separate* TCP connection, or should all of the requests and their corresponding responses be sent over the *same* TCP connection? In the former approach, the application is said to use **non-presistent connections**; and in the latter approach, **presistent connections**. HTTP uses presistent conections in its default mode, but clients and server can be configured to use non-presistent connection.

#### HTTP with Non-Persistent Connection

Steps of transferring a Web page from server to client for the case of non-presistent connections. Suppose the page consists of a base HTML file and 10 JPEG images, and all 11 of these objects reside on the same server. Further suppose the URL for the base HTML file is http://www.example.edu/folder/home.index

1.  The HTTP client process initiates a TCP connection to the server www.example.com on port number 80, which is the default port number for HTTP. Associated with the TCP connection, there will be a socket at the client and a socket at the server.
2.  The HTTP clients sends a HTTP request message to the server via its socket. The request message includes the path name `/folder/home.index`.
3.  The HTTP server process receives the request message via its socket, retrieves the object `/folder/home.index` from its storage, encapsulates the object in an HTTP response message, and sends the response message to the client via its socket.
4.  The HTTP server process tells TCP to close the TCP connection. (But the TCP doesn't actually terminate the connection until it knowns for sure that the client has received the response message intact.)
5.  The HTTP client receives the response message. The TCP connection terminates. The message indicates that the encapsulated object is an HTML file. The client extracts the file from the response message, examins the HTML file, and finds references to the 10 JPEG objects.
6.  The first four steps are then repeated for each of the referenced JPEG objects.

As the browser receives the Web page, it displays the page to the user. HTTP has nothing to do with how a Web page is interpreted by a client. The HTTP specifications define only the communication protocol between the client HTTP program and the server HTTP program.

Each TCP connection transports exactly one request message and one response message. Thus, in this example 11 TCP connections are generated.

User can configure modern browsers to control the degree of TCP connection parallelism. In their default modes, most browsers open 5 to 10 parallel TCP connections.

**Round-trip time** (RTT) is defined as the time it takes for a small packet to travel from client to server and then back to the client. The RTT includes packet-propagation delays, packet-queuing delays in intermediate routers and switches, and packet-processing delays.

When the user clicks on a hyperlink which causes the browser to initiate a TCP connection between the browser and Web server, this involves a "three-way handshake":

1.  The clients sends a small TCP segment to the server.
2.  The server acknowledges and responds with a small TCP segment.
3.  The client acknowledges back to the server.

The first two parts of the three-way handshake take one RTT. After completing the first two parts of the handshake, the client sends the HTTP request message combined with the third part of the three-way handshake (the acknowledgement) into the TCP connection. Once the request message arrives at the server, the server sends the HTML file into the TCP connection. This HTTP request/response eats up another RTT. Thus, roughly, the total response time is two RTTs plus the transmisison time at the server of the HTML file.

#### HTTP with Persistent Connections

Shortcomings of non-persistent connections:

-   A brand-new connection must be established and maintained for each *requested object*. For each of these connections, TCP buffers must be allocated and TCP variables must be kept in both the client and server. This can place a significant burden on the Web server, which may be serving requests from hundreds of different clients simultaneously.
-   Each object suffers a delivery delay of two RTTs--one RTT to establish the TCP connection and one RTT to request and receive an object.

With HTTP 1.1 persistent connections, the server leaves the TCP connection open after sending a response. Subsequent requests and responses between the same client and server can be sent over the same connection. Moreover, multiple Web pages residing on the same server can be sent from the server to the same client over a single persistent TCP connection. These requests for objects can be made back-to-back, without waiting for replies to pending requests (pipelining). Typically, the HTTP server closes a connection when it isn't used for a certain time (a configurable timeout interval). When the server receives the back-to-back requests, it sends the objects back-to-back. The default mode of HTTP uses persistent connections with pipelining. Most recently, HTTP/2 builds on HTTP 1.1 by allowing multiple requests and replies to be interleaved in the *same* connection, and a mechanism for prioritizing HTTP message requests and replies within this connection.

### 2.2.3 HTTP Message Format

The HTTP specifications include the definitions of the HTTP message formats. There are two types of HTTP messages, request messages and response messages.

#### HTTP Request Message 

A typical HTTP request message:

```
GET /somedir/page.html HTTP/1.1
Host: www.someschool.edu
Connection: close
User-agent: Mozilla/5.0
Accept-language: fr
```

-   The message is written in ordinary ASCII text, so ordinary computer-literate human being can read it.
-   The message consists of five lines, each followed by a carriage return and a line feed. The number of lines can vary from 1 to many.
-   The first line of an HTTP request message is called the **request line**.
    -   The request line has three fields: the method field, the URL field, and the HTTP version field.
    -   The method field can take on several different values, including `GET`, `POST`, `HEAD`, `PUT`, and `DELETE`.
    -   The great majority of HTTP request messages use the `GET` method.
-   The subsquent lines are called the **header lines**.
    -   The header line `Host: www.someschool.edu` specifies the host on which the object resides.
    -   By including the `Connection: close` header line, the browser is telling the server that it doesn't want to bother with persistent connections; it wants the server to close the connection after sending the requested object.
    -   The `User-agent:` header line specifies the user agent is Mozilla/5.0, a Firefox browser. This header line is useful because the server can actually send different versions of the same object to different types of user agents.
    -   Finally, the `Accept-language:` header indicates that the user prefers to receive a French version of the object. It is just one of many content negotiation headers available in HTTP.

![General format of an HTTP request message](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/http_request.jpeg)

The entity body is empty with the `GET` method, but is used with the `POST` method. An HTTP cliend often uses the `POST` method when the user fills out a form. With a `POST` message the user is still requesting a Web page from the server, but the specific contents of the Web page depends on what the user entered into the form fields. If the value of the method is `POST`, then the entity body contains what the user entered into the form fields.

It is not necessory to use the `POST` method when a request g enetrated with a form. The inputted data can be included in the reequested URL as extended URLs.

The `HEAD` method is similar to the `GET` method. When a server receives a request with the `HEAD` method, it responds with an HTTP message but it leaves out the requested objest. It can be used for debugging. The `PUT` method is often used in conjunction with Web publishing tools. It allows a user to upload an object to a specific path on a specific Web server. Also the `DELETE` works in the same way.

#### HTTP Response Message

```
HTTP/1.1 200 OK
Connection: close
Date: Tue, 18 Aug 2015 15:44:04 GMT
Server: Apache/2.2.3 (CentOS)
Last-Modified: Tue, 18 Aug 2015 15:11:03 GMT
Content-Length: 6821
Content-Type: text/html

(data data data data ...)
```

This response message has three sections: an initial **status line**, six **header lines**, and then the **entity body**. The status line has three fields: the protocol version field, a status code, and a corresponding status message.

The server uses the `Connection: close` header line to tell the client that it is going to close the TCP connection after sending the message. The `Date:` header line indicates the time and date when the HTTP response was created and sent by the server. The `Server:` header line indicates that the message was generated by an Apache Web server. The `Last-Modified:` header line indicates the time and date when the object was created or last modified. It is critical for object caching, both in the local client and in network cache servers. The `Content-Length:` header line indicates the number of bytes in the object being sent. The `Content-Type:` header line indicates that the object in the entity body is HTML text (and not by the file extension).

Some common status codes and associated phrases include:

-   `200 OK`: Request succeeded and the information is returned in the response.
-   `301 Moved Permanently`: Requested object has been permanently moved; the new URL is specified in `Location:` header of the response message. The client software will automatically retrieve the new URL.
-   `400 Bad Request`: This is a generic error code indicating that the request could not be understood by the server.
-   `404 Not Found`: The requested document does not exist on this server.
-   `505 HTTP Version Not Supported`: The requested HTTP protocol version is not supported by the server.

![General format of an HTTP response message](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/http_response.jpeg)

### 2.2.4 User-Server Interaction: Cookies

HTTP servers are stateless. It is often desirable for a Web site to identify users, either because the server wishes to restrict user access or because it wants to serve content as a function of the user identity. For these purposes, HTTP uses cookies. Cookies, defined in [RFC 6265], allow sites to keep track of users. Most major commercial Web sites use cookies today.

Cookie technology has four components:

-   A cookie header line in the HTTP response message.
-   A cookie header line in the HTTP request message.
-   A cookie file kept on the user's end system and managed by the user's browser.
-   A back-end database at the Web site.

![Keeping user state with cookies.](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/cookies.jpeg)

The first time a user visits a site, the user can provide a user identification (possibly his or her name). During the subsequent sessions, the browser passes a cookie header to the server, thereby identifying the user to the server. Cookies can thus be used to create a user session layer on top of stateless HTTP. Cookies can also be considered as an invasion of privacy.

### 2.2.5 Web Caching

A **Web cache**--also called a **proxy server**--is a network entity that satisfies HTTP request on the behalf of an origin Web server. The Web cache has its own disk storage and keeps copies of recently requested objects in this storage. Once a browser is configured, each browser request for an object is first directed to the Web cache:

1.  The browser establishes a TCP connection to the Web cache and sends an HTTP request for the object to the Web cache.
2.  The Web cache checks to see if it has a copy of the object stored locally. If it does, the Web cache returns the object within an HTTP response message to the client browser.
3.  If not, the Web cache opens a TCP connection to the origin server and sends an HTTP request for the object into the cache-to-server TCP connection. After receiving this request, the origin server sends the object within an HTTP response to the Web cache.
4.  When the Web cache receives the object, its stores a copy in its local storage and sends a copy, within an HTTP response message, to the client browser (over the existing TCP connection between the client browser and the Web cache).

Typically a Web cache is purchased and installed by an ISP.

Web caching has seen deployment in the Internet for two reasons:

-   It can substantially reduce the response time for a client request.
-   It can substantially reduce traffic on an institution's (for example, a company or a university) access link to the Internet.
-   It can substantially reduce Web traffic in the Internet as a whole, thereby improving performance for all applications.

Through the use of **Content Distribution Networks** (**CDNs**), Web caches are increasingly playing an important role in the Internet.

#### The Conditional GET

There is a mechanism called the **conditional GET** allows a cache to verify its objects are up to date. An HTTP request message is a so-called conditional GET message if (1) the request message uses the `GET` method and (2) the request message includes an `If-Modified-Since:` header line. An example:

First, a procy cache sends a request message to a Web server:

```
GET /fruit/kiwi.gif HTTP/1.1
Host: www.exotiquecuisine.com
```

Second, the Web server sends a response message with the requested object to the cache:

```
HTTP/1.1 200 OK
Date: Sat, 3 Oct 2015 15:39:29
Server: Apache/1.3.0 (Unix)
Last-Modified: Wed, 9 Sep 2015 09:23:24
Content-Type: image/gif

(data data data ...)
```

One week later, another browser requests the same object via the cache, the cache performs an up-to-date check by issuing a conditional GET. Specifically, the cache sends:

```
GET /fruit/kiwi.gif HTTP/1.1
Host: www.exotiquecuisine.com
IF-modified-since: Wed, 9 Sep 2015 09:23:24
```

This conditional GET is telling the server to send the object only if the object has been modified since the specified date. If the object has not been modified since 9 Sep 2015 09:23:24. Then the Web server sends a response message to the cache:

```
HTTP1/1 304 Not Modified
Date: Sat, 10 Oct 2015 15:39:29
Server: Apache/1.3.0 (Unix)

(empty eitity body)
```

## 2.3 Electronic Mail in the Internet

Let's have a high level view of the Internet mail system and its key components.

There are three components: user agents, mail servers, and the **Simple Mail Transfer Protocol** (**SMTP**). User agents allow user to read, reply to, forward, save, and compose messages. User agents send the message to the mail server, where the message is placed in the mail server's outgoing message queue. When someone wants to read a message, the user agent retrieves the message from the mailbox in the mail server.

Mail servers form the core of the e-mail infrastructure. Each recipient has a **mailbox** located in one of the mail servers. Mailbox manages and maintains the messages the have teen sent to it. A typical message starts its journey in the sender's user agent, travels to the sender's mail server, and travel to the recipient's mail server, where iti s deposited in the recipient's mailbox. When someone wants to access the messages in the mailbox, the mail server authenticates that person. Sender's mail server also deal with failures in recipient's mail server. Sender's mail server holds the message in a **message queue** and attempts to transfer the message later.

SMTP is the principal application-layer protocol for Internet electronic mail. It uses the reliable data transfer service of TCP to transfer mail from the sender's mail server to the recipient's mail server. The sender's mail server is the client side, and the recipients mail server is the server side.

### 2.3.1 SMTP

SMTP, defined in RFC 5321, is at the heart of Internet electronic mail. Ubiquity in the Internet, but a legacy technology that possesses certain archaic characteristics. It restricts the body of all mail messages to simple 7-bit ASCII.

SMTP does not normally userintermediate mail servers for sending mail, even when the two mail servers are located at opposite ends of the world.

The client SMTP server has TCP establish a connection to port 25 (plaintext) at the server SMTP. If the server is down, the clients tries again later. Once this connection is established, the server and client perform some application-layer handshaking. During this SMTP handshaking phase, the SMTP client indicates the e-mail address of the sender and the e-mail address of the recipient. Once the SMTP client and server have introduced themselves to each other, the client sends the message. SMTP can count on the reliable data transfer service of TCP to get the message to the server without errors.

An example transcript of messages exchanged between an SMTP client (C) and an SMTP server (S). The hostname of the client is `crepes.fr` and the hostname of the server is `hamburger.edu`.

```
S: 220 hamburger.edu
C: HELO crepes.fr
S: 250 Hello crepes.fr, pleased to meet you
C: MAIL FROM: <alice@crepes.fr>
S: 250 alice@crepes.fr ... Sender ok
C: DATA
S: 354 Enter mail, end with "." on a line by itself
C: Do you like ketchup?
C: How about pickles?
C: .
S: 250 Message accepted for delivery
C: QUIT
S: 221 hamburger.edu closing connection
```

As part of the dialogue, the client issued five commands: `HELO`, `MAIL FROM`, `RCPT TO`, `DATA`, and `QUIT`. These commands are self-explanatory. The client also sends a line consisting of a single period, which indicates the end of the message to the server. (In ASCII jargon, each message ends with `CRLF.CRLF`.) The server issues replies to each command, which each reply having a reply code and some (optional) English-language explanation. SMTP uses persistent connections: if the sending mail server has several messages to send to the same receiving mail server, it can send all of the messages over the same TCP connection. For each message, the client begins the process with a new `MAIL FROM:`, designates the end of message with an isolated period, and issues `QUIT` only after all messages have been sent.

### 2.3.2 Comparison with HTTP

Both protocols are used to transfer files from one host to another: HTTP transfers files (objects) from a Web server to a Web client; SMTP transfers files (e-mail messages) from one mail server to another mail server. When transferring the files, both persistent HTTP and SMTP use persistent connections.

There are import differences:

-   First HTTP is mainly a **pull protocol**--someone loads information on a Web server and users use HTTP to pull the information from the server at their convenience. In particular, the TCP connection is initiated by the machine that wants to receive the file. On the other hand, SMTP is primarily a **push protocol**--the sending mail server pushes the file to the receiving mail server. In particular, the TCP connection is initiated by the machine that wants to send the file.

-   The second difference is that SMTP requires each message, including the body of each message, to be 7-bit ASCII format. If the message contains characters that are not 7-bit ASCII or contains binary data, then the message has to be encoded into 7-bit ASCII. HTTP data does not impose this restriction.
-   A third important difference concerns how a document consisting of text and images (along with possibly other media types) is handled. HTTP encapsulates each object in its own HTTP responses message. SMTP places all of the messages's objects into one message.

### 2.3.3 Mail Message Formats

E-mail also uses header to contain peripheral information. This peripheral information is contained in a series of header lines. The header lines and the body of the message are separated by a blank line. RFC 5322 specifies the exact format for mail header lines as well as their semantic interpretations. As with HTTP, each header line contains readable text, consisting a keyword followed by a colon followed by a value. Every header must have a `From:` header line and a `To:` header line; a header may include a `Subject:` header line as well as other optional header lines. It is important to note that these header lines are *different* from the SMTP commands we studied in Section 2.4.1. The commands in that section were part of the SMTP handshaking protocol; the header lines examined in this section are part of the mail message it self.

A typically message header:

```
From: alice@crepes.fr
To: bob@hamburger.edu
Subject: Searching for the meaning of life.
```

After the message header, a blank line follows; then the message body follows.

### 2.3.4 Mail Access Protocols

Once SMTP delivers the message from the client side to the server side, the message is placed in recipient's mailbox. Up until the early 1990s a user reads mail by logging onto the server host and then executing a mail eader that runs on that host. Today, mail access uses a client-server architecture--the typical user reads e-mail with a client that executes on the user's end system. By executing a mail client on a local PC, users enjoy a rich set of features, including the ability to view multimedia messages and attachments.

A typical user runs a user agent on the local PC but accesses its mailbox stored on an always-on shared mail server. This mail server is shared with other users and is typically maintained by the user's ISP.

Alice's user agent uses SMTP to push the e-mail message into her mail server, then Alice's mail server uses SMTP to relay the e-mail message to Bob's mail server. Bob's user agent can't use SMTP bo obtain the message because obtaining the msessages is a pull operation, whereas SMTP is a push protocol. Bob's user agent has to use a mail access protocol to access the e-mail message from Bob's mail server. There are a number of popular mail access protocols, including **Post Office Protocol--Version 3 (POP3), Internet Mail Access Protocol (IMAP)**, and HTTP.

#### POP3

POP3 is an extremely simple mail access protocol, which is short and quite readable. POP3 begins when the user agent opens a TCP connection to the mail server on port 110. With the TCP connection established, POP3 progresses through three phases: authorizaiton, transaction, and update. During the authorization phase, the user agent sends a username and a password (in the clear) to authenticate the user. During the transaction phase, the user agent can mark messages for deletion, remove deletion marks, and obtain mail statistics. The update phase occurs after the client has issued the quit command, ending the POP3 session; at this time, the mail server deletes the messages that were marked for deletion.

In a POP transaction, the user agent issues commands, and the server responds to each command with a reply. There are two possiblie responses: `+OK` (sometimes followed by server-to-client data), used by the server to indicate that the previous commend was fine; and `-ERR`, used by the server to indicate that something was wrong with the previous command.

The authorization phase has two principal commands: `user <username>` and `pass <password>`. An example of using Telnet to connect a POP server:

```
telnet mailServer 110
+OK POP3 server ready
user bob
+OK
pass hungry
+OK user successfully logged on
```

A user agent using POP3 can offen be configured (by user) to "download and delete" or to ""download and keep." The sequence of commands issued by a POP3 user agent depends on which of these two modes the user agent is operating in. In the download-and-delete mode, the user agent will issue the `list`, `retr`, and `dele` commands. A transaction will look something like:

```
C: list
S: 1 498
S: 2 912
S: .
C: retr 1
S: (blah blah ...
S: ... ... ...
S: ... ... blah)
S: .
C: dele 1
C: retr 2
S: (blah blah ...
S: ... ... blah)
S: .
C: dele 2
C: quit
S: +OL POP3 server signing off
```

The user agent first asks the mail server to list the size of each of the stored messages. The user agent then retrieves and deletes each message from the server. Note that, after the authorization phase, the user agent employed only four commands: `list`, `retr`, `dele` and `quit`. The syntax is defined in RFC 1939. After processing the `quit` command, the POP3 server enters the update phase and removes messages 1 and 2 from the mailbox.

The download-and-delete mode partitions user's messages over multiple machines. In the download-and-keep mode, user can access a message from multiple machines.

The PPO3 server keeps track of which user messages have been marked deleted, but does not carry state information across POP3 sessions.

#### IMAP

The POP3 protocol does not provide any means for a user to create remote folders and assign messages to folders. To solve this and other problems, the IMAP protocol was invented. It has many more features than POP3, but it is also significantly more complex.

An IMAP server will associate each message with a folder. When a message firest arrives at the server, it is associated with the recipient's INBOX folder. The recipient can then move the message into a new, user-created folder, read the message, delete the message, and so on. The IMAP protocol provides commands to allow users to create folders and move messages from one folder to another. It also provides commands that allow users to search remote folders for messages matching specific criteria. Unlike POP3, an IMAP server maintains user state information across IMAP sessions.

Another important feature of IMAP is that it has commands that permit a user agent to obtain components of messages.

#### Web-Based E-mail

In this service the user agent is an ordinary Web browser, and the user communicates with its remote mailbox via HTTP. And the mail server, however, still sends messages to, and receives messages from, other mail servers using SMTP.

## 2.4 DNS--The Internet's Directory Service

One of the identifiers for a host is its **hostname**, such as `www.facebook.com`, `www.google.com`. Hostnames provide little information about the location within the Internet of the host, and it is difficult to process by routers. So hosts are also identified by so-called **IP address**.

An IP address consists of four bytes and has a rigid hierarchical structure. As we scan the IP address from left to right, we obtain more and more specific information about where the host is located in the Internet.

### 2.4.1 Services Provided by DNS

In order to reconcile the difference preferences between human and router on hostname identifier, we need a directory service that translates hostnames to IP addresses. This is down by the Internet's **domain name system**. The DNS is (1) a distributed database implemented in a hierarchy of **DNS servers**, and (2) an application-layer protocol that allows hosts to query the distributed database. The DNS servers are often UNIX machines running the Berkeley Internet Name Domain (BIND) software. The DNS protocol runs over UDP and uses port 53.

DNS is commonly employed by other application-layer protocols--including HTTP and SMTP to translate user-supplied hostnames to IP addresses. When a HTTP client sends a HTTP request message to request `www.someschool.edu/index.html`:

1.  The same user machine runs the cliend side of the DNS application.
2.  The browser extracts the hostname, `www.someschool.edu`, from the URL and passes the hostname to the client side of the DNS application.
3.  The DNS cliend sends a query containing the hostname to a DNS server.
4.  The DNS client eventually receives a reply, which includes the IP address for the hostname.
5.  Once the browser receives the IP address from DNS, it can initiate a TCP connection to the HTTP server process located at port 80 at that IP address.

DNS adds an additional delay to the Internet applications that use it. Fortunately, the desired IP address is often cached in a "nearby" DNS server, which helps to reduce DNS network traffic as well as the average DNS delay.

DNS provides a few other important services in addition to translating hostnames to TP addresses:

-   **Host aliasing**. A host with complicated hostname can have one or more alias names. A hostname such as `relay1.west-coast.enterprise.com` could have two aliases such as `enterprise.com` ans `www.enterprise.com`. In this case, the hostname `relay1.www-coast.enterprise.com` is said to be a **canonical hostname**. DNS can be invoked by an application to obtain the canonical hostname for a supplied alias hostname as well as the IP address of the host.
-   **Mail server aliasing**. For obvious reasons, it is highly desirable that e-mail addresses be mnemonic. The canonical hostname can be much complicate then `yahoo.com`. DNS can be invoked by a mail application to obtain the canonical hostname for a supplied alias hostname as well as the IP address of the host. In fact, the MX record permits a company;s mail server and Web server to have identical (aliased) hostnames; for example, a company's Web server and mail server can both be called `enterprise.com`.
-   **Load distribution**. DNS is also used to perform load distribution among replicated servers. Busy sites are replicated over multiple servers, with each server running on a different end system and each having a different IP address. 
-   for replicated Web servers, a *set* of IP addresses is thus associated with one canonical hostname. The DNS databases contains this set of IP addresses. When clients make a DNS query for a name mapped to a set of addresses, the server responds with the entire set of IP addresses, but rotates the ordering of the addresses within eacy reply. Because a client typically sends its HTTP request message to the IP address is listed first in the set, DNS rotation distributes the traffic among the replicated servers. DNS rotation is also used for e-mail so that multiple mail servers can have the same alias name. Also content distribution companies such as Akamai have used DNS in more sophisticated ways to provide Web content distribution.

### 2.4.2 Overview of How DNS Works

We will focus on the hostname-to-IP-address translation service.

Suppor an application running in a user's host needs to translate a hostname to an IP address. The application will invoke the client side of DNS, specifying the hostname that needs to be translated. (On many UNIX-based machines, `gethostbyname()` is the function call that an application calls in order to perform the translations.) DNS in the user's host then takes over, sending a query message into the network. All DNS query and reply messages are sent within UDP datagrams to port 53. After a delsy, ranging from milliseconds to seconds, DNS in the user's host receives a DNS reply message that provides the desired mapping. This mapping is then passed to invoking application. Thus, from the perspective of the invoking application in the user's host, DNS is a black box providing a simple, straightforward translatino service. But in fact, the black box that implements the service is complex, consisting of large number of DNS servers distributed around the globe, as well as an application-layer protocol that specifies how the DNS servers and querying hosts communicate.

A simple design for DNS would have one DNS server that contains all the mappings. In this certralized design, clients simply direct all queries to the single DNS server, and the DNS server responds directly to the querying clients. Although the simplicity of this design is attractive, it is inappropriate for today's Internet, with its vast (and growing) number of hosts. The problems with a centralized design include:

-   **A single point of failure**.
-   **Traffic volume**.
-   **Distant centralized database**.
-   **Maintenance**.

In a summary, a centralized database in a single DNS server simply *doesn't scale*. Consequently, the DNS is distributed by design. In fact, the DNS is a wonderful example of how a distributed database can be implemented in the Internet.

#### A distributed, Hierarchical Database

In order to deal with the issue of scale, the DNS uses a large number of servers, organized in a hierarchical fashion and distributed around the world. No single DNS server has all of the mappings for all the hosts in the Internet. To a first approximation, there are three classes of DNS servers--root DNS servers, top-level domain (TLD) DNS servers, and authoritative DNS servers--organized in a hierarchy as shown in the figure below. 

![Portion of hierarchy of the DNS servers.](https://github.com/yipeng-git/study_notes/raw/main/markdown_images/dns_hierarchy.jpeg)

Suppose a client wants to determine the IP address for the hostname `www.amazon.com`. To a first approximation, the client contacts one of the root servers, which returns IP address for TLD servers for the top-level domain `com`. The client then contacts one of these TLD servers, which returns the IP address of an authoritative server for `amazon.com`. Finally, the client contacts one of the authoritative server for `amazon.com`, which returns the IP address for the hostname `www.amazon.com`. We will soon examine this DNS lookup process in more detail. But lets first take a closer look at these t hree classes of DNS servers:

-   **Root DNS server**. There are 1086 as of 2 July 2020. These root name servers are managed by 13 different organizations. Root name servers provide the IP addresses of the TLD servers.
-   **Top-level domain (TLD) servers**. For each of the top-level domains--top-level domains such as com, org, net, edu, and gov, and all of the contry top-level domains--there is TLD server (or server cluster). These TLD servers are maintained by different companies. TLD servers provide the IP addresses for authoritative DNS servers.
-   **Authoritative DNS servers**. Every organization with publicly accessible hosts on the Internet must provide publicly accessible DNS records that map the names of those hosts to IP addresses. An organization can chose to implement its own authoritative DNS server to hold these records; or can pay to have these records stored in an authoritative DNS server of some service provider. Most universities and large companies implement and maintain their own primary and secondary authoritative DNS server.

There is another important type of DNS server called the **local DNS server**. A local DNS server does not strictly belong to the hierarchy but is nevertheless central to the DNS architecture. When a host connects to an ISP, the ISP provides the host with the IP addresses of one or more of its local DNS servers (typically through DHCP). When a host makes a DNS query, the query is sent to the local DNS server, which acts a proxy, forwarding the query into the DNS server hierarchy.

#### DNS Caching

DNS servers using **DNS caching** to improve the delay performance and to reduce the number of DNS messages ricocheting arount the Internet. DNS servers thus reduce the query chain by mapping the cached hostname/IP address pair, and discard cached information after a period of time.

### 2.4.3 DNS Records and Messages

**Resource records** (**RRs**) are the hostname-to-IP address mapping that stored in the DNS distributed database. 

A resource record is a four-tuple that contains the following fields:

```
(Name, Value, Type, TTL)
```

`TTL` is the time to live of the resource record; it determines when a resource should be removed from a cache.

Type:

-   If `Type=A`, then `Name` is a hostname and `Value` is the IP address for the hostname.
-   If `Type=NS`, then `Name` is a domain and `Value` is the hostname of an authoritative DNS server that knows how to obtain the IP addresses for hosts in the domain. This record is used to route DNS queries further along in the query chain.
-   If `Type=CNAME`, then `Value` is a canonical hostname for the alias hostname `Name`. This record can provide querying hosts the canonical name for a hostname.
-   If `Type =MX`, then `Value` is the canonical name of a mail server that has an alias hostname `Name`. MX records the hostnames of mail servers to have simple aliases. Note that by using the MX record, a company can have the same aliased name for its mail server and for one of its other servers. To obtain the canonical name for the mail server, a DNS client would query for an MX record; to obtain the canonical name for the other server, the DNS client would query for the CNAME record.

#### DNS Messages

There are two kinds of DNS messages, the query and reply messages. Both query and reply messages have the same format. The semantics of the various field in a DNS message are as follows:

-   The first 12 bytes is the *header section*, which has a number of fields. The first field is a 16-bit number that identifies the query. This identifier is copied into the reply message to a query, allowing the client to match received replies with sent queries. There are a number of flags in the flag field. A 1-bit query/reply flag indicates whether the message is a query (0) or a reply (1). A 1-bit authoritative flag is set in a reply message when a DNS server is an authoritative server for a queried name. A 1-bit recursion-desired flag is set when a client desires that the DNS server perform recursion when it doesn't have the record. A 1-bit recursion-available field is set in a reply if the DNS supports recursion. In the header, there are also four number of fields indicate the number of occurrences of the four types of data sections that follow the header.
-   The *question section* contains information about the query that is being made. This section includes (1) a name field that contains the name that is being queried, and (2) a type field that indicates the type of question.
-   In a reply message, the *answer section* contains the resource reccords for the name that was orginanlly queried. A reply can return mutiple Res in the answer, since a host name can have mutiple IP addresses.
-   The *additional section* contains other helpful records. For example, the answer field in a reply to an MX query contains a resource record providing the canonical hostname of a mail server. The addtional section contains a Type A record providing the IP address for the canonical hostname of the mail server.

**Nslookup program** can be used to send a DNS query message directly from the host you're working on.

#### Inserting Records into the DNS database

First register the domain name at a **registrar**, which is a commercial entity that verifies the uniqueness of the domain name and enters the domain name into the DNS database, and collects a small fee from you for its services.

You want makesure type A, type NS, type MX to be inserted.

## 2.5 Peer-to-Peer File Distribution

The applications described thus far, including the Web, e-mail, and DNS, all employ client-server arthitechture with significant reliance on always-on infrastructure servers. With a P2P architecture, there is a minimal (or no) reliance on always-on infrastructure servers. Instead, pairs of intermittently connected hosts, called peers, communicate directly with each other. These peers are not owned by a service provider, but are instead desktops and laptops controlled by users.

In P2P file distribution, each peer can redistribute any portion of the file it has received to any other peers, thereby assisting the server in the distribution process. As of 2016, the most popular P2P file distribution protocol is BitTorrent, originally developed by Bram Cohen.

#### Scalability of P2P Architectures

In the client-server architecture, the distribution time increases linearly and without bound as the number of peers increases. However, for the P2P architecture, the minimum distribution time is not only always less than the distribution time of the client-server architecture; it is also less than a constant time for *any* number of peers *N*. Thus, applications with the P2P architecture can be self-scaling. This scalability is a direct consequence of peers being redistributors as well as consumers of bits.

#### BitTorrent

In BitTorrent, the collection of all peers participating in the distribution of a particular file is called a *torrent*. Peers in a torrent download equal-size *chunks* of the file from one another, with a typical chunk size of 256 kbytes. When a peer first joins a torrent, it has no chunks. Over time it accumulates more and more chunks. While it downloads chunks it also uploads chunks to other peers. Once a peer has acquired the entire file, it may (selfishly) leave the torrent, or (altruistically) remain in the torrent and continue to upload chunks to other peers. Also, any peer may leave the torrent at any time with only a subset of chunks, and later rejoin the torrent.

Each torrent has an infrastructure node called *tracker*. When a peer joins a torrent, it registers itself with the tracker and periodically informs the tracker that it is still in the torrent. In this manner, the tracker keeps track of the peers that are participating in the torrent. A given torrent may have fewer than ten or more than a thousand peers participating at any instant of time.

When a new peer joins the torrent, the tracker randomly selects a subset of peers from the set of participating peers, and sends the IP addresses of these 50 peers to the new peer. Possessing this list of peers, the new peer attempts to establish concurrent TCP connections with all the peers on this list. 

At any given time, each peer will have a subset of chunks from the file, with different peers having different subsets. Periodically, the peer will ask each of its neighboring peers for the list of the chunks they have. When requesting chunks, a peer uses a technique called **rarest first**. The peer will request the rarest chunks among neighbors first. This manner makes the rarest chunks get more quickly redistributed, aiming to equalize the number of copies of each chunk in the torrent.

To determine which errquests a peer should responds to, BitTorrent uses a clever trading algorithm. The peer continually measures the rate at which it receives bits and determines the four peers that are feeding it at the highest rate. The peer reciprocates by sending chunks to these same four peers. Every 10 seconds, recalculates the rates and possibly modified the set of four peers. In BitTorrent lingo, these four peers are said to be **unchoked**. Importantly, every 30 seconds, the peer also picks one additional neighbor at random and sends it chunks. This randomly chosen peer is said to be **optimistically unchoked** in BitTorrent lingo. If two peers are satisfied with the trading, they will put each otehr in their top four lists and continue trading with each other until one of the peers finds a better partner. The effect is that peers capable of uploading at compatible rates tends to find each other. The random neighbor selection also allows new peers to get chunks, so that they can have something to trade. All other neighboring peers besides these five peers are "choked", that is they do not receive any chunks from the peer. 

This incentive mechanism for trading is often referred to as tit-for-tat. It has been shown that this incentive scheme can be circumvented. Nevertheless, the BitTorrent ecosystem is wildly successful, with millions of simultaneous peers actively sharing files in hundreds of thousands of torrents.

Another application of P2P is Distributed Hast Table (DHT). It is a simple database, with the database records being distributed over the peers in a P2P system. DHTs have been widely implemented (e.g. in BitTorrent) and have been subject of extensive research.

## 2.6 Video Streaming and Content Distribution Networks

Streaming prerecorded video now accounts for the majority of the traffic in residential ISPs in North America. The Netflix and YouTube services along consumed a whopping 37% and 16%, respectively, of residential ISP traffic in 2015.

### 2.6.1 Internet Video

The prerecorded videos are placed on servers, and users send requests to the server to view the video *on demand*.

A video is a sequence of images, typically being displayed at a constant rate, for example at 24 or 30 images per second. An uncompressed, digitally encoded image consists of an array of pixels, with each pixel encoded into a number of bits to represent luminance and color. An important characteristic of video is that it can be compressed, thereby trading off video quality with bit rate. Today's off-the-shelf compression algorithms can compress a video to essentially any bit rate desired.

2.6.2 HTTP Streaming and DSAH

In HTTP streaming, the video is simply stored at an HTTP server as an ordinary file with a specific URL. When a user wants to see the video, the client establishes a TCP connection with the server and issues an HTTP `GET` request for that URL. The server then sends the video file, within an HTTP response message, as quickly as the underlying network protocols and traffic condition will allow. On the client side, the bytes are collected in a client application buffer. Once the number of bytes in this buffer exceeds a predetermined threshold, the client application begins playback--specifically, the streaming video application periodically grabs video frams from the client application buffer, decompresses the frames, and display them on the user's screen. Thus, the video streaming application is displaying video as it is receiving and buffering frames corresponding to the latter parts of the video.

HTTP streaming has a major shortcoming: All clients receive the same encoding of the video, despite the large variation in the amount of bandwidth available to a client, both across different clients and slao over time for the same client. This has led to the development of a new type of HTTP-based streaming, often referred to as **Dynamic Adaptive Streaming over HTTP (DASH)**. In DASH, the video is encoded into several different versions, with each version having a different bit rate and, correspondingly, a different quality level. The client selects different chunks one at a time with `HTTP GET` request message.

The HTTP server also has a **manifest file**, which provides a URL for each version along with its bit rate. The client first request the manifest file and learns about the various versions, then selects one chunk at a time by specifying a URL and a byte range in an `HTTP GET` request message for each chunk. While downloading chunks, the client also measures the received bandwidth and runs a rate determination algorithm to select the chunk to request next.

### 2.6.3 Content Distribution Networks

For a Internet video company, perhaps the most staightforward approach to providing streaming video service is to build a single massive data center, store all of its videos and stream the videos directly from data center to clients worldwide. But there are three major problems: 1) Long communicaiton links with annoying freezing delays. 2) Popular video will likely be send many times over the same communication links, which waste network bandwidth and is costly for the Internet video company to pay for the traffic. 3) A single data center represents a single point of failure.

There is a solution called **Content Distribution Networks (CDNs)**. A CDN manages servers in multiple geographically distributed locations, stores copies of the videos (and other types of Web content, including documents, images, and audio) in its servers, and attempts to direct each user request to a CDN location that will provide the better user exprience. The CDN may be a **private CDN**, that is owned by the content provider itself. The CDN may alternatively be a **third-party CDN** that distributs content on behalf of multiple content providers.

CDNs typically adopt one of two different server placement philosophies:

-   **Enter Deep**. One philosophy, pionnered by Akamai, is to *enter deep* into the access networks of Internet Service Providers, by deploying server clusters in access ISPs all over the world. Akamai takes this approach with clusters in approximately 1700 locations. The goal is to get close to end users, thereby improving user-perceived delay and throughput by decreasing the number of links and routers between the end user and the CDN server from which it receives content. But maintaining and managing the clusters becomes challenging.
-   **Bring Home**. Another design philosophy, taken by Limelight and many other CDN companies, is to *bring the ISPs home* by building large clusters at a smaller number (for example, tens) of sites. Instead of getting inside the access ISPs, these CDNs typically place their cluster in Internet Exchange Points (IXPs). Compared with the enter-deep design philosophy, the bring-home design typically returns in lower maintenance and management overhead, possibly at the the expense of higher delay and lower throughput to end users.

Many CDNs do not push videos to their clusters but use a simple pull strategy: Similar to Web caching.

#### CDN Operation

When a client is instructed to retrieve a specific video (URL), the CDN must intercept the request so that it can (1) determine a suitable CDN server cluster for that client at that time, and (2) redirect the client's request to a server in that  cluster.

Most CDNs take advantage of DNS to intercept and redirect requests. A simple example to illustrate how the DNS is typlically involved. Suppose a content provider, NetCinema, employs the third-party CDN company, KingCDN, to distribute its videos to its customers. On the NetCinema Web pages, each of its videos is assigned a URL that includes the string "video" and a unique identifier for the video itself. Then six steps occur:

1.  The user visits the Web page at NetCinema.
2.  When the user clicks on the link, the user's host sends a DNS query for video.netcinema.com.
3.  The user's Local DNS Server (LDNS) relays the DNS query to an authoritative DNS server for NetCinema, which observers the string "video" in the hostname video.netcinema.com. To "hand over" the DNS query to KingCDN, instead of returning an IP address, the NetCinema authoritative DNS server returns to the LDNS a hostname in the KingCDN's domain, for example, a1105.kingcdn.com.
4.  From this point on, the DNS query enters into KingCDN's private DNS infrastructure. The user's LDNS then sends a second query, now for a1105.kingcdn.com, and KingCDN's DNS system eventually returns the IP addresses of a KingCDN content server to the LDNS. It is thus there, within the KingDSN's DNS system, that the CDN server from which the client will receive its content is specified.
5.  The LDNS forwards the IP address of the content-serving CDN node to the user's host.
6.  Once the client receives the IP address for a KingCDN content server, it estibalishes a direct TCP connection with the server at that IP address and issues an HTTP GET request for the video. If DASH is used, the server will send to the client a manifest file with a list of URLs, one for each version of the video, and the client will dynamically select chunks from the different versions.

#### Cluster Selection Strategies

At the core of any CDN deployment is a **cluster selection strategy**, a mechanism for dynamically directing clients to a server cluster or a data center within the CDN. CDNs generally employ proprietary cluster selection strategies.

One simple strategy is to assign the client to the cluster that is **geographically closest**. Using commercial geo-location databases and MaxMind, each LDNS IP address is mapped to a geographic location. The DNS chooses the geographically closest cluster from the client. Such a solution can work reasonably well for a large fraction of the clients. However, for some clients, the solution may perform poorly, since the geographically closest cluster may not be the closest cluster in terms of the length of number of hops of the network path. Furthermore, a problem inherent with all DNS-based approaches is that some end-users are configured to use remotely located LDNSs, in which case the LDNS location may be far from the client's location. Moreover, this simply strategy ignores the variation in delay and available bandwidth over time of Internet paths, always assigning the same cluster to a particular client.

In order to determine the best cluster for a client based on the *current* traffic conditions, CDNs can instead perform periodic **real-time measurements** of delay and loss performance between their clusters and clients. For instance, a CDN can have each of its clusters periodically send probes to all of the LDNSs around the world. One drawback of this approach is that many LDNSs are configured to not respond to such probes.

### 2.6.4 Case Studies: Netflix, YouTube, and Kankan

#### Netflix

Netflix has a Web site that handles numerous functions, including user registration and login, billing, movie catalogue for browsing and searching, and a movie recomendation system. This Web site run entirely on Amazon server in the Amazon cloud. Additionally, the Amazon cloud handles the following critical functions:

-   ***Content ingestion***. Before Netflix can distribute a movie to its customer, it must first ingest and process the movie. Netflix receives studio master versions of movies and upload them to hosts in the Amazon cloud.
-   ***Content processing**. The machines in the Amazon cloud create many different formats for each movie, suitable for a diverse array of client video player running on desktop computers, smartphones, and game consoles connected to televisions. A different version is created for each of these formats and at mutiple bit rates, allowing for adaptive streaming over HTTP using DASH.
-   ***Uploading versions to its CDN***. Once  all of the versions of a movie have been created, the hosts in the Amazon cloud upload the versions to its CDN.

When Netflix first rolled out its video streaming service in 2007, it employed three third-party CDN companies to distribute its video content. Netflix has since created its own private CDN, from which it now streams all of its videos (Netflix still uses Akamai to distribute its Webpages, however.) Netflix has installed server racks both in IXPs and within residential ISPs themselves. Netflix currently has server racks in over 50 IXP locations. There are also hundreds of ISP locations housing Netflix racks. Each server in the rack has several 10 Gbps Ethernet ports and over 100 terabytes of storage. IXP installations often contains the entire Netflix streaming video library, including multiple versions of the videos to support DASH; local IXPs may only have one server and contains only the most popular videos. Netflix does not use pull-caching, but distributes by pushing the videos to its CDN servers during off-peak hours. Netflix pushes only the most popular videos on a day-to-day basis.

Since Netflix uses its own private CDN, which distributes only video, Netflix has been able to simplify and tailor its CDN design. In particular, Netflix does not need to employ DNS redirect, instead, the Netflix software on the Amazon cloud directly tells the client to use a particular CDN server. Furthermore, the Netflix CDN uses push caching rather than pull caching.

#### YouTube

Similar to Netflix, Google uses its own private CDN to distribute YouTube videos, and has installed server clusters in many hundreds of different IXP and ISP locations. Google distributes YouTube videos from these locations and directly from its huge datacenters. Unlike Netflix, Google uses pull caching and DNS redirect. Most of the time, Google's cluster-selection strategy directs the client to the cluster for which the RTT between client and cluster is the lowest; however, in order to balance the load across clusters, sometimes the client is directed to a more distant cluster.

YouTube employs HTTP streaming, often making a small number of different versions available for a video, each with a different bit rate and corresponding quality level. YouTube does not employ adaptive streaming (such as DASH), but instead requires the user to manually select a version. In order to save bandwidth and server resources that would be wasted by repositioning or early termination, YouTube uses the HTTP byte range request to limit the flow of transmitted data after a terget of amount of video is prefetched.

YouTube uploaders also upload their videos from client to server over HTTP. YouTube processes each video it receives, converting it to a YouTube video format and creating multiple versions at different bit rate. This processing takes place entirely within Google data centers.

#### Kankan

There is another approach uses P2P delivery instead of (or along with) client-server delivery. Since 2011, Kankan (owned and operated by Xunlei) has deploying P2P video delivery with great success.

At a high level, P2P video streaming is very similar to BitTorrent file downloading. When a peer wants to see a video, it contact a tracker to discover other peers in the system that have a copy of that video. This requesting peer then requests chunks of video in parallel from the other peers that having the video. Different from downloading with BitTorrent, however, requests are preferentially made for chunks that are to be played back in the near future in order to ensure continuous playback.

Recently, Kankan has migrated to a hybrid CDN-P2P streaming system. Specifically, Kankan now deploys a few hundred servers within China ans pushes video content to these servers. This Kankan CDN plays a major role in the start-up stage of video streaming. In most cases, the client requests the beginning of the content from CDN servers, and in parallel requests content from peers. When the total P2P traffic is sufficient for video playback, the client will cease streaming from the CDN and only stream from peers. But if P2P streaming traffic becomes insufficient, the client will restart CDN connections and return to the mode of hybrid CDN-P2P streaming. In this manner, Kankan can ensure short initial start-up delays while minimally relying on costly infrastructure servers and bandwidth.

## 2.7 Socket Programming: Creating Network Applications

### 2.7.1 Socket Programming with UDP

The sender's IP address and port number are attached by the OS, not by UDP application. The destination address and port should be attached to the packet before dropping the packet to the socket.

#### UDPClient.py

```python
from socket import *
serverName = 'hostname'
serverPort = 12000
clientSocket = socket(AF_INET, SOCK_DGRAM) # AF_INET indicates IPv4 network, SOCK_DGRAM indicates UDP socket
message = raw_input('Input lowercase sentence:') # py build-in function for user input
clientSocket.sendto(message.encode(), (serverName, serverPort))
modifiedMessage, serverAddress = clientSocket.recvfrom(2048) # buffer size is 2048 bytes
print(modifiedMessage.decode())
clientSocket.close()
```

#### UDBServer.py

```python
from socket import *
serverPort = 12000
serverSocket = socket(AF_INET, SOCK_DGRAM)
serverSocket.bind(('', serverPort)) # bind port 12000
print("The server is ready to receive.")
while True:
  	message, clientAddress = serverSocket.recvfrom(2048) # receives from port 12000, the clientAddress contains both the IP and port
    modifiedMessage = message.decode().upper()
    serverSocket.sendto(modifiedMessage.encode(), clientAddress)
```

### 2.7.2 Socket Programming with TCP

Connection-oriented protocol. Need to handshake and establish a TCP connection. The IP addresses and port numbers are associate with the TCP connection, so no need to attach the destination address to the packet before dropping it into the socket.

#### TCPClient.py

```python
from socket import *
serverName = 'servername'
serverPort = 12000
clientSocket = socket(AF_INET, SOCK_STREAM) # IPv4 and TCP socket
clientSocket.connect((serverName, serverPort)) # estibalish TCP connection
sentence = raw_input('Input lowercase sentence: ')
clientSocket.send(sentence.encode())
modifiedSentence = clientSocket.recv(1024)
print('From Server: ', modifiedSentence.decode())
clientSocket.close()
```

#### TCPServer.py

```python
from socket import *
serverPort = 12000
serverSocket = socket(AF_INET, SOCK_STREAM)
serverSocket.bind(('', serverPort))
serverSocket.listen(1) # listen for TCP connection requests on port 12000
print('The server is ready to receive.')
while True:
  	connectionSocket, addr = serverSocket.accept() # complete handshakes and creating a TCP connection
  	sentence = connectionSocket.recv(1024).decode()
  	capitalizedSentence = sentence.upper()
  	connectionSocket.send(capitalizedSentence.encode())
  	connectionSocket.close()
```



# 3. Transport Layer

## 3.1 Introduction and Transport-Layer Services

Transport-layer protocol provides for **logical communication** between application processe srunning on different hosts. By *logical communication*, we mean that from application's perspective, it is as if the hosts running the processes were directly connected; in reality, the hosts may be on opposite sides of the planet, connected via numerous routers and a wide range of link types. Application processes use the logical communication provided by the transport layer to send messages to each other, free from the worry of details of the physical infrastructure used to carry these messages.

Transport-layer protocols are implemented in the end systems but not in network routers. On the sending side, transport layer converts the application-layer messages it receives into transport layers packets, known as transport-layer **segments**. This is done by breaking the application messages into smaller chunks and adding a transport-layer header to each chunk to create the transport-layer segment. The transport-layer then passes the segment to the network layer at the sending system, where the segment is encapsulated within a network-layer packet (a datagram) and send to the destination. Network routers act only on the network-layer fields of the datagram.

### 3.1.1 Relationship Between Transport and Network Layers

Transport-layer lies just above the network layer in the protocol stack. It provides logical communication between *processes* running on different hosts, and a network layer protocol provides logical communication between *hosts*. This distinction is subtle but important.

### 3.1.2 Overview of the Transport Layer in the Internet

**UDP** provides an unreliable, connectionless service to the invoking application. **TCP** provides a reliable, connection-oriented service to the invoking application.

The transport-layer packets are referred as *segment*. However, the Internet literature (for example, the RFCs) also refers to the transport-layer packet for TCP as a segment but often refers to the packet for UDP as a datagram. But it also uses the term *datagram* for the network-layer packet!

The Internet's network-layer protocol has a name--IP, for Internet Protocol. IP provides logical communication between hosts. The IP service model is a **best-offert delivery service**. This means that IP makes its "best effort" to deliver segments between communication hosts, *but it makes no guarantees*. In particular, it does not guarantee segment delivery, it does not guarantee orderly delivery of segments, and it does not guarantee the integrity of the data in the segments. IP is said to be an **unreliable service**. Every host has at least one network-layer address, a so-called IP address.

THe fundamental responsibility of UDP and TCP is to extend IP's delivery service between two end systems to delivery service between two processes running on the end systems. Extending host-to-host delivery to process-to-process delivery is called **transport-layer multiplexing** and **demultiplexing**. UDP and TCP also provide integrity checking by including error-detection fields in their segments' headers. These two minimal transport-layer services--process-to-process data delivery and error checking--are the only two services that UDP provides! UDP is an unreliable service.

TCP offers several additional services to applications. First and foremost, it provides **reliable data transfer**. Using flow control, sequence numbers, acknowledgements, and timers, TCP ensures that data is delivered from sending process to receiving process, correctly and in order. TCP thus convert's IP's unreliable service between end systems into a reliable data transport service between processes. TCP also provides **congestion control**. It is a servivce for the Internet as a whole, a service for the general good. TCP strives to give each connection traversing a congested link an equal share of the link bandwidth. This is done by regulating the rate at the sending side. UDP traffic, is unregulated.

## 3.2 Multiplexing and Demultiplexing

The transport layer has the responsibility of delivering the data in segments to the appropriate application process running in the host. A process can have one or more **sockets**, which is an interface allows data passes from the process to the network. Thus, the transport layer in the receiving host does not actually deliver data directly to a process, but instead to an intermediary socket. Each socket has a unique identifier. The format of the identifier depends on whether the socket is a UDP or a TCP socket.

Each transport-layer segment has a set of fields in the segment to direct an incoming transport-layer segment to the appropriate socket. At receiving end, the transport layer examines these fields to identify the socket. This job of delivering the data in a transport-layer segment to the correct socket is called **demultiplexing**. The job of gathering data chunks at the source host from different sockets, encapsulating each data chunk with header information (that will later be using in demultiplexing) to create segments, and passing the segments to the network layer is called **multiplexing**.

Transport-layer multiplexing requires (1) that sockets have unique identifiers, and (2) that each segment have special fields that indicate the socket to which the segment is to being delivered. These special fields are the **source port number field** and the **destination port number field**. Each port number is a 16-bit number, ranging from 0 to 65535. The port numbers ranging from 0 to 1023 are called **well-known port numbers** and are restricted, which means that they are reserved for use by well-known application protocols such as HTTP (port 80) and FTP (port 21).

### Connectionless Multiplexing and Demultiplexing

Typically, the client side of the application lets the transport layer automatically (and transparently) assign the port number, whereas the server side of the application assigns a specific port number.

If two UDP segments have different source IP address and/or source port numbers, but have the same *destination* IP address and *destination* port number, then the two segments will be directed to the same destination process via the same distination socket.

### Connection-Oriented Multiplexing and Demultiplexing

TCP socket is identified by a four-tuple: (source IP address, source port number, destination IP address, destination port number).

In particular, and in contrast with UDP, two arriving TCP segments with different source IP addresses or source port numbers will be directed to two different sockets.

The server host may support many simultaneous TCP connection sockets, with each socket attached to a process, and with each socket identified by its own four-tuple.

### Web Servers and TCP

Today's high-performing Web servers often use only one process, and create a new. thread with a new connection socket for each new client connection.

## 3.3 Connectionless Transport: UDP

UDP does just about as little as a transport protocol can do. Aside from the multiplexing/demultiplexing function and some light error checking, It adds nothing to IP. With UDP there is no handshaking between sending and receiving transport-layer entities before sending a segment. For this reason, UDP is said to be *connectionless*.

DNS is a great example of application-layer protocol that typically uses UDP.

Some application prefer UDP for the following reasons:

-   *Finer application-level control over what data is sent, and when*. Under UDP, there is no congestion control that throttles the sender. TCP will also continue to resend a segment until the receipt of the segment has been acknowledged by the destination, regardless of how long reliable delivery takes. Real-time applications often require a minimum sending rate and do not want to overly delay segment transmission, and can tolerate some data loss.
-   *No connection establishment*. UDP does not introduce any delay to establish a connection.
-   *No connection state*. TCP maintains connection state in the end system. This connection state includes receive and sned buffers, congestion-control parameters, and sequence and acknowledgement number parameters. UDP, on the other hand, does not maintain connection state and does not track any of these parameters. For this reason, a server devoted to a particular applciation can typically support many more active clients when the application runs over UDP rather than TCP.
-   *Small packet header overhead*. The TCP segment has 20 bytes of header overhead in every segment, whereas UDP has only 8 bytes of overhead.

Multimedia application sometimes can tolerate a small amount of packet loss. Furthermore, real-time application, like Internet phone and video conferencing, react very poorly to TCP's congestion control. When packet loss rates are low, and with some organization blocking UDP traffic for security reason, TCP becomes a increasingly attractive protocol for streaming media support.

UDP has no congestion control, there would be som much packet overflow at routers that very few UDP packets would successfully traverse the source-to-destination path. The high loss rates induced by the uncontrolled UDP senders would cause the TCP senders to dramatically devrease their rates. Thus, the pack of congestion control in UDP can result in high loss rates between a UDP sender and receiver, and the crowding out of TCP sessions.

It *is* possible for an apllication to have reliable data transfer when using UDP. This can be done if reliability is built into the application itself.

### 3.3.1 UDP Segment Structure

The application data occupies the data field of the UDP segment. The UDP header has only four fields, each consisting of two bytes. The port numbers allow the destination host to pass the application data to the correct process running on the destination end system. The length field specifies the number of bytes in the UDP segment (header plus datai). An explicit length value is neede since the size of the data field may differ from one UDP segment to the next. The checksum is used by the receiving host to check whether errors have been introduced into the segment.

![UDP segment structure](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/udp_structure.jpeg)

### 3.3.2 UDP Checksum

## 3.4 Principles of Reliable Data Transfer

The figure below illustrate the framework for our study of reliable data transfer. With a reliable channel, no transferred data bits are corrupted or lost, and all are delivered in the order in which they were sent. This is precisely the service model offered by TCP to the Internet application that invoke it.

It is the responsibility of a **reliable data transfer protocol** to implement this service abstraction. This task is made difficult by the fact that the layer *below* the reliable data transfer protocol may be unreliable.

One assumption we'll adopt throughout our discussion here is that packets will be delivered in the order in which they were sent, with some packets possibly being lost; thst is the underlying channel will not reorder packets. 

![Reliable data transfer: Service model and service implementation](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/reliable_data_transfer.jpeg)

Here `rdt` stands for *realiable data transfer* protocol and `udt` stands for *unreliable data transfer* protocol.

In the following we use the terminology "packet" rather than transport-layer "segment". Because the theory developed in this section applies to computer networks in general and not just to the Internet transport layer, the generic term "packet" is perhaps more appropriate here.

In this section we consider only the case of **unidirectional data transfer**, that is, data transfer from the sending to the receiving side. The case of reliable **bidirectional** (that is, full-duplex) **data transfer** is conceptually no more difficult but considerably more tedious to explain.

### 3.4.1 Building a Reliable Data Transfer Protocol

#### Reliable Data Transfer over a Perfectly Reliable Channel: `rdt1.0`

Simplest case, in which the underlying channerl is completely reliable. The **finite-state machine (FSM)** definition for the `rdt 1.0` sender and receiver are shown in the figure below. It is important to note that there are separate **FSMs** for the sender and for the receiver.

![rdt1.0 - A protocol for a complete reliable channel](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/rdt1.0.jpeg)

In this simple protocol, there is no difference between a unit of data and a packet. Also, all packet flow is from the sender to receiver; with a perfectly reliable channel there is no need for the receiver side to provide any feedback to the sender since nothing can go wrong! Note that we have also assumed that the receiver is able to receive data as fast as the sender happens to send data. Thus, there is no need for the receiver to ask the sender to slow down!

#### Reliable Data Transfer over a Channel with Bit Errors: `rdt2.0`

A more realistic model of the underlying channel is one in which bits in a packet may be corrupted. Such bit errors typically occur in the physical components of a network as a packet is transmitted, propagates, or is buffered. We'll continue to assume for the moment that all transmitted packets are received in the order in which they were sent.

A message-dictation protocol uses both **positive acknowledgements** ("OK") and **negative acknowledgements** ("Please repeat that."). These control messages allow the receiver to let the sender know what has been received correctly, and what has been received in error and thus requires repeating. In a computer network setting, reliable data transfer protocols based on such retransmission are known as **ARQ (Automatic Repeat reQuest) protocols**.

Fundamentally, three additional protocol capabilities are required in ARQ protocols to handle the presence of bit errors:

-   *Error detection.* First, a mechanism is needed to allow the receiver to detect when bit errors have occurred. These techniques require that extra bits be sent from the sender to the receiver; these bits will be gathered into the packet checksum field of the `rdt2.0` data packet.
-   *Receiver feedback*. The positive (ACK) and negative (NAK) acknowledgement replies in the message-dictation scenario are examples of such feedback. Our `rdt2.0` protocol will similary send ACK and NAK packets back from the receiver to the sender. In pricinple, these packets need only be one bit long; for example, a 0 value could indicate a NAK and a value of 1 could indicate an ACK.
-   *Retransmission*. A packet that is received in error at the receiver will be retransmitted by the sender.

The figure below shows the FSM representation of `rdt2.0`, a data transfer protocol employing error detection, positive acknowledgements, and negative acknowledgements.

![rdt2.0 - A protocol for a channel with bit errors](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/rdt2.0.jpeg)

It is important to note that when the sneder is in the wait-for-ACK-or-NAK state, it *cannot* get more data from the upper layer. Thus, the sender will not send a new piece of data untio it is sure that the receiver has correctly received the current packet. Because of this behavior, protocols such as `rdt2.0` are known as **stop-and-wait** protocols.

Protocol `rdt2.0` may look as if it works but, unfortunately, it has a fatal flaw. In particular, we haven't accounted for the possibility that the ACK or NAK packet could be corrupted! Minimally, we will need to add checksum bits to ACK/NAK packets in order to detect such errors. The more difficult question is how the protocol should recover from errors in ACK or NAK packets. The difficulty here is that if an ACK or NAK is corrupted, the sender has no way of knowing wether or not the receiver has correctly received the last piece of transmitted data.

Consider three possiblilities for handling corrupted ACKs or NAKs:

-   For the first possibility, the speaker would probably ask, "What did you say?"
-   A second alternative is to add enough checksum bits to allow the sender not only to detect, but also to recover from, bit errors. This solves the immediate problem for a channel that can corrupt packets but not lose them.
-   A third approach is for the sender simply to resend the current data packet when it receives a garbled ACK or NAK packet. This approach, however, introduces **duplicate packets** into the sender-to-receiver channel. The fundamental difficulty with duplicate packets is that the receiver doesn't know whether the ACK or NAK *it* last sent was received correctly at the sender. Thus, it cannot know *a priori* whether an arriving packet contains new data or is a retransmission!

A simple solution to this new problem (and one adopted in almost all existing data transfer protocols, including TCP) is to add a new field to the data packet and have the sender number its data packets by putting a **sequence number** into this field. The receiver then need only check this sequence number to determine whether or not the received packet is a retransmission. For this simple case of a stop-and-wait prpotocol, a 1-bit sequence number will suffice, since it will allow the receiver to know wether the sender is resending the previously transmitted packet or a new packet. Since we are currently assuming a channel that does not lose packets, ACK and NAK packets do not themselves need to indicate the swquence number of the packet they are acknowledging. The sender knowns that a received ACK or NAK packet (whether garbled or not) was generated in response to its most recently transmitted data packet.

The figure below show the FSM description for `rdt2.1`.

![rdt2.1 sender](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/rdt2.1_sender.jpeg)

![rdt2.1 receiver](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/rdt2.1_receiver.jpeg)

We can accomplish the same effect as a NAK if, instead of sending a NAK, we send an ACK for the last correctly received packet. A sender that receives two ACKs for the same packet (that is, receives **duplicate ACKs**) knowns that the receiver did not correctly receive the packet following the packet that is being ACKed twice. Our NAK-free reliable data transfer protocol for a channel with bit errors is `rdt2.2`, shown in the figures below.

![rdt2.2 sender](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/rdt2.2_sender.jpeg)

![rdt2.2 receiver](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/rdt2.2_receiver.jpeg)

One subtle change between `rdt2.1` and `rdt2.2` is that the receiver must now include the sequence number of the packet being acknowledged by an ACK message (this is done by including the `ACK,0` or `ACK,1` argument in `make_pkt()` in the receiver FSM), and the sender must now check the sequence number of the packet being acknowledged by a received ACK message (this is done by including the `0` or `1` argument in `isACK()` in the sender FSM).

#### Reliable Data Transfer over a Lossy Channel with Bit Errors: `rdt3.0`

Suppose now that in addition to corrupting bits, the underlying channel can *lose* packets as well. Two additional concerns must now be addressed by the protocol: how to detect packet loss and what to do when packet loss occurs. The use of checksumming, sequence numbers, ACK packets, and retransmission--the techniques already developed in `rdt2.2`--will allow us to anser the latter concern. Handling the first concern will require adding a new protoocl mechanism.

There are many possible approaches. Here we'll put the burden of detecting and recovering from lost packets on the sender. Suppose that the sender transmits a data packet and either that packet, or the receiver's ACK of that packet, get lost.If the sender is willing to wait long enough so that it is *certain* that a packet has been lost, it can simply retransmit the data packet.

But how long ust the sender wait? The sender must clearly wait at least as long as a round-trip delay between the sender and receiver plus whatever amount of time is needed to process a packet at the receiver. In many networks, this worst-case maximum delay is very difficult even to estimate. Moreover, the protocol should ideally recover from packet loss as soon as possible. The approach thus adopted in practice is for the sender to judiciously choose a time value such that packet loss is likely, although not guaranteed. If an ACK is not received within this time, the packet is retransmitted. This introduces the possibility of **duplicate data packet** in the sender-to-receiver channel. Happily, protocol `rdt2.2` already has enough functionality to handle the case of duplicate packets.

In all cases, the action for the sender is the same: retransmit. Implementing a time-based retransmission mechanism requires a **countdown timer** that can interrupt the sender after a given amount of time has expired. The sender will thus need to be able to (1) start the timer each time a packet is sent, (2) respond to a timer interrupt, and (3) stop the timer.

The figure below shows the sender FSM for `rdt3.0`, a protocol that reliably transfer data over a channel that can corrupt or lose packets. Because packet sequence number alternate between 0 and 1, protocol `rdt3.0` is sometimes known as the **alternating-bit protocol**.

![rdt3.0 sender](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/rdt3.0_sender.jpeg)

### 3.4.2 Pipelined Reliable Data Transfer Protocols

Rather than operate in a stop-and-wait manner, the sender is allowed to send multiple packets without waiting for acknowledgements. This technique is known as **pipelining**. Pipelining has the following consequences for reliable data transfer protocols:

-   The range of sequence numbers must be increased, since each in-transit packet (not counting retransmissions) must have a unique sequence number and there may be multiple, in-transit, unacknowledged packets.
-   The sender and receiver sides of the protocols may have to buffer more than one packet. Minimally, the sender will have to buffer packets that have been transmitted but not yet acknowledged. Buffering of correctly received packets may also be needed at the receiver, as discussed below.
-   The range of sequence numbers needed and the buffering reequirements will depend on the manner in which a data transfer protocol responds to lost, corrupted, and overly delayed packets. Two basic approaches toward pipelined error recovery can be identified: **Go-Back-N** and **selective repeat**.

### 3.4.3 Go-Back-N (GBN)

In a **Go-Back-N (GBN) protocol**, the sender is allowed to transmit multiple packets without waiting for an acknowledgement, but is constrained to have no more than some maximum allowable number, N, of unacknowledged packets in the pipeline.

The figure below shows the sender's view of the range of sequence numbers in a GBN protocol. 

![Sender's view of sequence numbers in Go-Back-N](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/gbn_sequence.jpeg)

If we define `base` to the sequence number of the oldest unacknowledged packet and `nextsequm` to be the smallest unused sequence number (that is, the sequence number of the next packet to be sent), then four intervals in the range of sequence numbers can be identified. Sequence numbers in the interval `[0,base-1]` correspond to packets that have already been transmitted and acknowledged. The interval `[base,nextseqnum-1]` corresponds to packets that have been sent but not yet acknowledged. Sequence number in the interval `[nextseqnum,base+N-1]` can be used for packets that can be sent immediately, should data arrive from the upper layer. Finally, sequence number greater than or eequal to `base+N` cannot be used until an unacknowledged packet currently in the pipeline (the packet with sequence number `base`) has been acknowledged.

As the protocol operates, this window slides forward over the sequence number space. For this reason, *N* is often referred to as the **window size** and GBN protocol itself as a **sliding-window protocol**. 

In practice, a packet's sequence number is carried in a fixed-length field in the packet header. If *k* is the number of bits in the packet sequence number field, the range of sequence number is thus `[0,2^k-1]`. Recall that `rdt3.0` had a 1-bit sequence number and a range of sequence numbers of `[0,1]`. We will see that TCP has a 32-bit sequence number field, where TCP sequence numbers counts bytes in the byte stream rather than packets.

The figures below shows the the extended FSM description of the sender and receiver sides of an ACK-based, NAK-free, GBN protocol.

![Extended FSM description of the GBN sender](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/gbn_sender.jpeg)

![Extended FSM description of the GBN receiver](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/gbn_receiver.jpeg)

We refer to this FSM as *extended FSM* because we have added variables for `base` and `nextseqnum`, and added operations on these variables and conditional actions involving these variables.

The GBN sender must response to three types of events:

-   *Invocation from above*. When `rdt_send()` is called from above, the sender first checks to see if the window is full. If the window is full, the sender simply returns the data back to the upper layer, an implicit indication that the window is full. The upper layer would presumably then have to trey again later. In real implementation, the sender would more likely have either buffered (but not immediately send) this data, or would have a synchronization mechanism that would allow the upper layer to call `rdt_send()` only when the window is not full.
-   *Receipt of an ACK*. In our GBN protocol, an acknowledgment for a packet with sequence number *n* will be taken to be a *cumulative acknowledgment*, indicating that all packets with a sequence number up to and including *n* have been correctly received at the receiver.
-   *A timeout event*. The protocol's name, "Go-Back-N", is derived from the sender's behavior in the presence of lost or overly delayed packets. As in the stop-and-wait protocol, a timer will again be used to recover from lost data or acknowledgment packet. If a timeout occurs, the sender resends all packets that have been previously sent but that have not yet been acknowledged.

The. r eceiver's actions in GBN are also simple. If a packet with sequence number *n* is received correctly and is in order, the receiver sends an ACK for packet *n* and elivers the data portion of the packet to the upper layer. In all other cases, the receiver discards the packet and resends an ACK for the most recently received in-order packet.

In our GBN protocol, the receiver discards out-of-order packets. Although it may seem silly and wasteful to discard a correctly received packet, there is some justification for doing so. While the sender must maintain the upper and lower bounds of its window and position of `nextseqnum` within this window, the only piece of information the receiver need maintain is the sequence number of the next in-order packet.

It is worth noting that an implementation of this protocol in a protocol stack would likely have a structure similar to that of the extended FSM. The implementation would also likely be in the form of various procedures that implement the actions to be taken in response to the various events that can occur. In such **event-based programming**, the various procedures are called (invoked) either by other procedures in the protocol stack, or as the result of an interrupt. In the sender, these events would be (1) a call from the upper-layer entity to invoke `rdt_sent()`, (2) a timer interrupt, and (3) a call from the lower lalyer to invoke `rdt_rcv()` when a packet arrives.

### 3.4.4 Selective Repeat (SR)

There are, however scenarios in which GBN itself suffers from performance problems. In particular, when the window size and bandwidth-delay product are both large, many packetts can be in the pipeline. A single packet error can thus cause GBN to retransmit a large number of packets, many unnecessarily. As the probability of channel errors increases, the pipeline can become filled with these unnecessary retransmissions.

As the name suggests, selective-repeat protocols avoid unnecessary retransmissions by having the sender retransmit only those packets that it suspects were received in error at the receiver. This individual retransmisison will require that the receiver *individually* acknowledge correctly received packets. A window size of *N* will again be used to limit the number of outstanding, unacknowledged packets in the pipeline. However, unlike GBN, the sender will have already received ACKs for some of the packets in the window.

![Selective-repeat (SR) sender and receiver views of sequence-number space](https://raw.githubusercontent.com/yipeng-git/study_notes/main/markdown_images/selective_repeat.jpeg)

SR sender events and actions:

-   *Data received from above*. When data is received from above, the SR sender checks the next available sequence number for the packet and decides to accept or reject the data.
-   *Timeout*. Timer are again used to protect against lost packets. However, each packet must have its own logical timer.
-   *ACK received*. If an ACK is received, the SR sender marks that packet as having been received, provided it is in the window. If the packet's sequence number is equal to `send_base`, the window b ase is moved forward to the unacknowledged packet with the smallest sequence number.

SR receiver events and actions:

-   *Packet with sequence number in* `[rcv_base, rcv_base+N-1]` *is correctly received*. Send selective ACK to the sender. If `seqnum` equals to `rcv_base`, deliver the packet to the upper layer and move the window. 
-   *Packet with sequence number in* `[rcv_base-N, rcv_base-1]` is correctly received. In this case, an ACK must be generated, even though this is a packet that the receiver has previously acknowledged.
-   *Otherwise*. Ignore the packet.