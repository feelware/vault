---
tags:
  - video-notes
src-date: 2024-09-13
src-author:
  - Eli Etherton
src-link:
  - https://youtu.be/0OztKsGTqos
---
# TCP/IP for Programmers

## Logical vs. Physical

- Logical device: specific service (firewall, router, modem, access point, etc)
- Physical device: the actual object you can touch and plug into the network
- Multiple logical devices are now built into a single device (SOHO router: router, switch, access point, firewall and even VPN at the same time)
- Design/whiteboard based on logic. Build based on physical

## Beware of cacheing

- Systems (routers, etc) cache data
- When you make a change, the system you're connecting to may still respond with cached data
- Replication time: how long it takes for changes to be copied to all relevant systems

## Protocols

- Languages shared by systems to talk to each other
- Network protocols, storage protocols, communication protocols

## Ethernet

- Topology: Star
- Connector: RJ45
- Cable: Twisted pair
- Identifiers: MAC addresses

### Layer 2 devices

- Hub: prone to broadcast storms
- Bridge: connects two hubs and controls traffic between them, still not a good solution
- Switch: "every port is a bridge"
	- MAC address table: maps ports to the MAC addresses of the devices connected to them
	- Back-plane: Overall throughput of the switch

[more info](../../projects/unmsm-2025-0/redes-expo-ethernet.md)

## Internet layer


