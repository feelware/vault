---
tags:
  - "#textbook-notes"
  - wip
src-date: 2007-01-01
src-author:
  - William Stallings
src-link: "[[../../source-material/textbooks/data-computer-communications-william-stallings.pdf|data-computer-communications-william-stallings]]"
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

1. The input bit sequence $m$, buffered in the source's memory, is turned into a digital signal $g(t)$ (those same bits represented by voltage changes over time) ![](../../utilities/attachments/Pasted%20image%2020241223180539.png)
2. $g(t)$ is converted into an analog signal $s(t)$ that can be sent through the telephone line
3. The signal inevitably loses fidelity when travelling, so the received signal $r(t)$ is different from the transmitted signal $s(t)$ to some degree
4. $r(t)$ is converted back from an analog to digital, resulting in $g'(t)$, which will be different from $g(t)$ to some degree
5. The received sequence of bits $m'$ is buffered in the destination's memory

![Simplified Data Communications Model](../../utilities/attachments/Pasted%20image%2020241223174818.png)

### Networks

#### Wide Area Networks (WAN)

Cover a large geographical area. Nodes are not concerned with the content of the data transmitted, just in making sure they reach their destination. #wip

Some technologies to implement WANs:
- Circuit switching: Dedicated path between two stations (e.g. telephone network)
- Packet switching: Data is sent as a sequence of packets. About 64 kbps
- Frame relay: Leverages high data rates and low error rates of modern transmission facilities. Up to 2 Mbps
- ATM: Evolution of frame relay. In the Gbps range

#### Local Area Networks (LAN)

Smaller geographical data. #wip

#### Wireless Networks

#wip

### The Internet

> [..] Vint Cerf and Bob Kahn of ARPA started to develop methods and protocols for *internetworking*; that is, communicating across arbitrary, multiple, packet-switched networks. They published a very influential paper in May of 1974 [CERF74] outlining their approach to a Transmission Control Protocol [...] eventually leading to the TCP (Transmission Control Protocol) and IP (Internet Protocol) protocols, which, in turn, formed the basis for what eventually became the TCP/IP protocol suite. This provided the foundation for the Internet.

#### Internet Service Provider (ISP)

Company that provides customers with presence on the internet

#### Customers Premises Equipment (CPE)

Telecommunications equipment at a customer's location

#### Central Office (CO)

ISP-managed end of communication line between customer and ISP

#### Point of Presence (POP)

#wip

#### Network Service Provider (NSP)

Company that provides ISPs with communication with other ISPs

#### Network Access Point (NAP)

Point of connection between many ISPs.


