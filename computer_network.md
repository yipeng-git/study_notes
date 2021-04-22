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

1.  The HTTP client process initiates a TCP connection to the server www.example.com on port number 80, which is the default port number for HTTP.l Associated with the TCP connection, there will be a socket at the client and a socket at the server.
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

