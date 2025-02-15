---
tags:
  - "#textbook-notes"
  - wip
src-date: 2007-01-01
src-author:
  - William Stallings
src-link: "[data-computer-communications-william-stallings](../../source-material/textbooks/data-computer-communications-william-stallings.pdf)"
---
# Data and Computer Communications

## Data Communications, Data Networks and the Internet

### A communications model

Transmitting information between two computers has a lot of intricacies that will be covered throughout the book. Some of them are listed below.

- Transmission system utilization
- Interfacing
- Signal generation
- Synchronization
- Exchange management
- Error detection and correction
- Flow control
- Addressing
- Routing
- Recovery
- Message formatting
- Security
- Network management

### Data communications

When sending mail from one computer to another through a telephone network, the information goes through a process like this:

1. The input bit sequence $m$, buffered in the source's memory, is turned into a digital signal $g(t)$ (those same bits represented by voltage changes over time)
2. $g(t)$ is converted into an analog signal $s(t)$ that can be sent through the telephone line
3. The signal inevitably loses fidelity when travelling, so the received signal $r(t)$ is different from the transmitted signal $s(t)$ to some degree
4. $r(t)$ is converted back from an analog to digital, resulting in $g'(t)$, which will be different from $g(t)$ to some degree
5. The received sequence of bits $m'$ is buffered in the destination's memory

![Simplified Data Communications Model](../../utilities/attachments/Pasted%20image%2020241223174818.png)

### Networks

#### Wide Area Networks (WAN)

Cover a large geographical area. Nodes are not concerned with the content of the data transmitted, just in making sure they reach their destination.

Some technologies to implement WANs:

- Circuit switching: Dedicated path between two stations (e.g. telephone network)
- Packet switching: Data is sent as a sequence of packets. About 64 kbps
- Frame relay: Leverages high data rates and low error rates of modern transmission facilities. Up to 2 Mbps
- ATM: Evolution of frame relay. In the Gbps range

### The Internet

> [..] Vint Cerf and Bob Kahn of ARPA started to develop methods and protocols for *internetworking*; that is, communicating across arbitrary, multiple, packet-switched networks. They published a very influential paper in May of 1974 [CERF74] outlining their approach to a Transmission Control Protocol [...] eventually leading to the TCP (Transmission Control Protocol) and IP (Internet Protocol) protocols, which, in turn, formed the basis for what eventually became the TCP/IP protocol suite. This provided the foundation for the Internet.

#### Internet Service Provider (ISP)

A company that provides customers with presence on the internet.

#### Customers Premises Equipment (CPE)

Telecommunications equipment at a customer's location.

#### Central Office (CO)

ISP-managed end of communication line between customer and ISP.

#### Point of Presence (POP)

#wip

#### Network Service Provider (NSP)

A company that provides ISPs with communication with other ISPs.

#### Network Access Point (NAP)

Point of connection between many ISPs.

## Protocol Architecture, TCP/IP, and Internet-Based Applications

### The TCP/IP Protocol Architecture

#### Layers

It makes sense to separate communications mechanisms into loosely coupled layers. Many of the needs presented in one layer are not affected by how the other layer implements it under the hood.

##### Physical layer

Manages **hardware transmission mediums**. Concerned with signals, data rate, and related matters. Implemented in end-systems and routers.

##### Network access layer

Concerned with transmission mechanisms **specific to the type of network to be used** (circuit switching, packet switching, etc). There are as many NAPs as the amount of networks the host/router is connected to (Router J has two NAPs, for instance). Implemented in end-systems and routers.

##### Internet layer

Needed when the source and destination are in **different networks** (like Host A and Host B, connected to Network 1 and 2 respectively). Implemented in end-systems and routers.

##### Transport layer

Exposes an API that **allows applications to send and receive data reliably**, so that developers don't have to implement those mechanisms every time.

> [...] the mechanisms for providing reliability are essentially independent of the nature of the applications.

##### Application layer

Any application's module concerned with data transmission and communication. Makes use of the API provided by the [transport layer](#Transport%20layer) and adds its own logic on top of it.

#### Operation of the TCP and IP

![TCP/IP concepts](../../utilities/attachments/Pasted%20image%2020250111213811.png)

- Network access protocol: Used to **connect a computer to a subnetwork**
- Internet Protocol (IP): Used to **move blocks of data** from one host to another, across one or multiple routers
- Transmission Control Protocol (TCP): Used to **ensure** that these blocks are delivered to the **right host**, to the **right process**, **reliably**

> [!note]
>  Two levels of entity addressing are needed:
>  - Each host should have an address unique within the Internet
>  - Each process should have an address unique within the host. These addresses are called **ports**

TCP receives user data and breaks it down into **TCP segments**. Then, each layer appends certain information to each segment.

![Protocol Data Units (PDUs) in the TCP/IP Architecture](../../utilities/attachments/Pasted%20image%2020250112210759.png)

1. **TCP header**, added by TCP (see [transport layer](#Transport%20layer)):
	- Destination port: which process should receive the data
	- Sequence number: a sequential number is assigned to each segment to ensure ordering
	- Checksum
2. **IP header**, added by the IP (see [internet layer](#Internet%20layer)):
	- Host address: which host should receive the data
3. **Network/packet header**, added by the [network access](#Network%20access%20layer) protocol:
	- Destination subnetwork address: #wip
	- Facilities requests (optional)

> At router J, the packet header is stripped off and the IP header examined. On the basis of the destination address information in the IP header, the IP module in the router directs the datagram out across subnetwork 2 to B. To do this, the datagram is again augmented with a network access header.

> When the data are received at B, the reverse process occurs. At each layer, the corresponding header is removed, and the remainder is passed on to the next higher layer, until the original user data are delivered to the destination process.

#### TCP and UDP

UDP is a much more minimal [transport layer](#Transport%20layer) protocol. UDP doesn't guarantee preservation of sequence, or protection against duplication, unlike TCP.
