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

