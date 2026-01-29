# Enterprise-WAN-Design

### Multi-Site Banking Network Simulation

This project demonstrates the design, configuration, and validation of an **enterprise-style Wide Area Network (WAN)** connecting multiple branch locations for a simulated banking environment.

The network was built in Cisco Packet Tracer and implements **LAN segmentation, inter-VLAN routing, dynamic routing, and layered security controls**, mirroring real-world enterprise network engineering and security practices.

---

## Project Objective

Design and deploy a secure, scalable WAN that connects **three branch LANs** while enabling full end-to-end communication across the organization.

The project required:

- Subnetting and IP addressing design
- VLAN segmentation
- Inter-VLAN routing
- Dynamic routing (OSPF)
- Network hardening and access controls
- Validation and testing of connectivity and security policies

The final solution reflects how production enterprise networks are architected and secured.

---

## Architecture Overview

### Topology
- 3 Routers (WAN core + branches)
- Multiple Layer 2 switches
- Multiple VLANs per LAN
- Endpoints representing users, servers, and guest devices

### High-Level Design
- Router-on-a-Stick for inter-VLAN routing
- OSPF for dynamic route propagation
- VLAN-based segmentation for security and performance
- Extended ACLs for traffic control
- Port security on access switches
- Secure remote management via SSH

---

## Technologies & Concepts Implemented

### Networking
- WAN architecture
- Subnetting & VLSM
- VLANs (10/20/30/100)
- 802.1Q trunking
- Inter-VLAN routing (router-on-a-stick)
- OSPF dynamic routing
- Static & default routes

### Security
- Extended Access Control Lists (ACLs)
- Port security (sticky MAC)
- SSHv2 remote management
- Console authentication
- Password encryption
- Device hardening best practices
- Segmented guest network isolation

### Validation
- End-to-end connectivity testing
- Routing table verification
- OSPF neighbor checks
- VLAN segmentation tests
- ACL enforcement tests

---

## Repository Structure
## Repository Structure

```
Enterprise-WAN-Design/
├── README.md
├── diagrams/
   └── topology.png
├── docs/
   ├── Network_Design_Document.md
   ├── IP_Addressing_Plan.md
   ├── VLAN_and_Trunking.md
   ├── Routing_and_OSPF.md
   ├── Security_Controls.md
   └── Validation_and_Testing.md
└── configs/
```
