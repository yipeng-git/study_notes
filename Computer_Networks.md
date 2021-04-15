# Computer Networks and the Internet
## What is the Internet?

-   Nuts-and-Bolts: The basic hardware and software components make up the internet.
-   Networking Infrastructure that provides services to distributed applications.

### A Nuts-and-Bolts Description

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

### A Services Description

-   Internet: *an infrastructure that provides services to applications*
-   **Distributed applications**: involves mutiple end systems that exchanges data with others. (Email, web surfing, IM, map, streaming)
-   End systems attached to the Internet provide a **socket interface** that specifies how a to deliver data to a specific destination on another end system. (a set of rules that the sending program must follow to deliver)

### What is a Protocol?

*A **protocol** defines the format and the order of messages exchanged between two or more communicatiing entites, as well as the actions taken on the transmission and/or receipt of a message or other event.*

## The Network Edge

-   End systems are referred to as *hosts* because they host (run) application programs. **End Systms = Hosts**
-   Hosts can be divided into **clients** and **servers**.
-   Today, most of the servers reside in large **data centers**.

### Access Networks

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
    -   

#### Avvess in the Enterprise (and the Home): Ethernet and WiFi

-   Local area network (**LAN**) is used to connect an end system to the edge router.
-   **Ethernet** is the most prevalent access technology in corporate, university, and home networks.
-   **WiFi** uses IEEE 802.11 standards.

#### Wide-Area Wireless Access: 3G and LTE

-   **LTE **= Long-Term Ebolution. It is actually not 4G, a miss used concept by the ISPs.

### Physical Media

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

## The Network Core

### Packet Switching

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

### Circuit Switching

There are two fundamental switches: **circuit switching** and **packet switching**. The sender and the receiver must establish a connection, and the network must reserve one circuit on each of the links. The switches on the path between the sender and receiver maintain connection state for circuit connection. Transmission rate is a guaranteed constant rate. This is a dedicated end-to-end connection between the two hosts. 

#### Multiplexing in Circuit-Switched Networks

-   A circuit in a link is implemented with either **frequency-division multiplexing (FDM)** or ** time-division multiplexing (TDM)**.
-   FDM divides the frequency spectrum of a link. Telephone networks usually use 4 kHz, which is called **bandwidth**.

#### Packet Switching vs Circuit Switching

### A Network of Networks

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

## Delay, Loss and Throughput in Packet-Switched Networks

Limited by physical laws.

### Over view of Delay in Packet-Switched Networks

The most important of these delays are the **nodal processing delay, queuing delay, transmission delay**, and **propagation delay**; together, these delays accumulate to give a **total nodal delay**.

#### Types of Delay

-   **Processing Delay** - the time required to examing the packet's header and determine where to direct the packet.
-   **Queuing Delay** - the time packet waits to be transmitted onto the link.
-   **Transmission Delay** - the amount of time required to push all of the packet's bits into the link.
-   **Propagation Delay** - the time required to propagate from the beginning of the link to the end of the link.

#### Comparing Transmisison and Propagation Delay

-   Depends on distance and link media.

### Queuing delay and Packet Loss

-   **Trafic intensity** - (average rate at which bits arrive at the queue) / (transmission rate).
    -   La/R > 1, arriving rate exceeds transmission rate.
    -   Not usually sufficient to fully charaterize the queuing delay statistics.

#### Packet Loss

When a packet arrives to find a full queue. With no place to store such a packet, a router will **drop** that packet; that is the packet will be **lost**.

### End-to-End Delay

Suppose there are N-1 routers between the source host and the destination host.

-   End-to-end delay = N * (dproc + dtrans + dprop)

#### Traceroute

Suppose there are N-1 routers. Then the source will send N special packets into the network towards the ultimate destination. When the nth router receives the Nth packet, the router does not forward the packet but returns a message back to the source including the name and address of the router. In this manner, the source can reconstruct the route taken by packets flowing from source to destination and can determine the rount-trip delays to all internet routers. Traceroute repeats the experiment three times.

#### End System, Application, and Other Delays

-   An end system may *Purposefully* delay its transmission as part of protocol for sharing the medium with other end systems.
-   Media packetization delay such as Voice-over-IP (VoIP). The sending side must first fill a packet with encoded digitized speech before passing the packet to the Internet.

### Throughput in Computer Networks

-   **Instantaneous throughput** - at any instant time.
-   **Average throughput** - time averaged.
-   Depends on the transmission rage of the **bottleneck link**.

## Protocol Layers and Their Service Models

Internet is an *extremely* complicated system.

### Layered Architecture



