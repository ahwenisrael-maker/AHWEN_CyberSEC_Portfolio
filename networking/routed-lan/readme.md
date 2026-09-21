# Routed Multi-Network LAN — Cisco Packet Tracer

## Overview

This project involved designing and configuring a small network containing two separate IP network segments connected through a router.

The topology consists of two switches connecting multiple end devices, with a router providing connectivity between the two networks.

The network was simulated using **Cisco Packet Tracer**.

---

## Project Objective

The objective was to build a functional network in which devices on separate IP networks could communicate through a router.

The project provided practical experience with:

* IPv4 addressing
* Subnet masks
* Router interfaces
* Ethernet switching
* Network segmentation
* Inter-network communication
* Connectivity testing

---

## Network Topology

![Network Topology](./topology.png)

The topology contains:

* 1 router
* 2 switches
* Multiple PCs
* Multiple laptops
* Two IP network segments

### Network 1

**Network:** `192.168.1.0/24`

Example hosts include:

* `192.168.1.10`
* `192.168.1.11`
* `192.168.1.12`
* `192.168.1.13`

### Network 2

**Network:** `10.10.10.0/8`

Example hosts include:

* `10.10.10.0`
* `10.10.10.1`
* `10.10.10.2`
* `10.10.10.3`

The router provides the connection between the two network segments.

---

## Connectivity Testing

Connectivity between hosts on the different network segments was tested using **ICMP ping**.

![Connectivity Test](./connectivity-test.png)

The test from a host on the `192.168.1.x` network to `10.10.10.3` produced successful replies, demonstrating communication between the two network segments.

The test showed:

* 4 packets sent
* 3 packets received
* 1 packet lost
* 25% packet loss

The successful responses demonstrated that traffic was able to traverse the configured network path.

---

## Key Networking Concepts

### IP Addressing

Hosts were assigned IPv4 addresses belonging to their respective network segments.

### Subnetting

Different IP networks were used to separate groups of devices into distinct network segments.

### Routing

A router was positioned between the two networks to allow traffic to move between them.

### Switching

Each group of end devices was connected through a network switch.

### ICMP

Ping was used to test whether hosts could successfully communicate across the network.

---

## Cybersecurity Relevance

Network architecture plays an important role in cybersecurity.

Separating devices into different network segments can help organisations control traffic flow and limit the potential impact of a compromised device.

The concepts demonstrated in this project provide a foundation for understanding:

* Network segmentation
* Attack surfaces
* Network reconnaissance
* Firewall placement
* Access control
* Network monitoring
* Traffic analysis

---

## Skills Demonstrated

* Cisco Packet Tracer
* IPv4 addressing
* Subnet masks
* Basic subnetting
* Routing concepts
* Switching concepts
* LAN design
* Network segmentation
* ICMP connectivity testing
* Basic network troubleshooting

---

## Key Takeaway

This project provided practical experience designing a network with multiple IP segments and using a router to facilitate communication between them.

It reinforced the relationship between **IP addressing, switching, routing, and end-to-end connectivity**.
