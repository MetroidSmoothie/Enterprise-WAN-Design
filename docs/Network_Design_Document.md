
# Network Design Document

## 1. Project Overview

This project implements a simulated three-site enterprise WAN using Cisco Packet Tracer. The network demonstrates multi-site connectivity, dynamic routing, VLAN segmentation, inter-VLAN routing, and infrastructure security controls.

The architecture consists of three interconnected routers, office LANs, and dedicated IPv4 subnets supporting departmental workstations and infrastructure services.

## 2. Network Architecture

### 2.1 Three-Site WAN Topology

The WAN connects three office locations through a triangular arrangement of serial links between routers R1, R2, and R3.

![Enterprise WAN Topology](../diagrams/Network_Topology.png)

The interconnected topology provides multiple potential routing paths between routers, supporting dynamic route selection through OSPF.

### 2.2 Site Architecture

| Location | Network Function | Infrastructure |
|---|---|---|
| Office 1 | Departmental network | Two switches, three VLANs, and inter-VLAN routing through R1 |
| Office 2 | Employee and guest network | Single LAN subnet connected through R3 |
| Office 3 | Administrative and server network | LAN hosting email, Syslog/NTP, and administrative systems through R3 |

## 3. LAN Architecture

### 3.1 Office 1 — VLAN Segmentation

Office 1 separates Management, Marketing, and Accounting workstations into three VLANs distributed across two interconnected switches.

IEEE 802.1Q trunking carries VLAN traffic between switches, while R1 provides inter-VLAN routing through dedicated router subinterfaces.

For the logical VLAN diagram, VLAN assignments, access-port mappings, and trunk connections, see **[VLAN and Trunking](VLAN_and_Trunking.md)**.

### 3.2 Office 2 — Employee and Guest Network

Office 2 uses a shared LAN subnet for employee and guest workstations.

An extended ACL on R3 restricts guest access to a designated infrastructure server in Office 3 while permitting other traffic.

### 3.3 Office 3 — Infrastructure Services

Office 3 hosts the email server, Syslog/NTP server, and an administrative workstation.

These resources connect to the enterprise WAN through R3 and are accessible according to the network's routing and access control configurations.

## 4. WAN Routing and IP Addressing

### 4.1 Dynamic Routing

OSPF Area 0 provides dynamic routing between R1, R2, and R3 across the interconnected serial WAN links.

The routing design enables the routers to exchange network reachability information and provides alternative routing paths within the triangular topology.

Detailed routing design and OSPF neighbor relationships are documented in [Routing and OSPF](Routing_and_OSPF.md).

### 4.2 IPv4 Addressing

The network uses the `172.16.10.0/24` address space, divided into eight `/27` subnets for the three WAN connections and five LAN/VLAN networks.

Interface addresses, subnet assignments, and endpoint addressing are documented in [IP Addressing Plan](IP_Addressing_Plan.md).

## 5. Security Architecture

Security controls are implemented at the network and device levels.

| Security Control | Implementation |
|---|---|
| Network segmentation | Dedicated VLANs and LAN subnets |
| Traffic filtering | Extended ACL restricting specified guest traffic |
| Switch port security | Sticky MAC address learning and port security |
| Secure remote management | SSHv2 and local authentication |
| Administrative access | Console and VTY access controls |

Implementation details are documented in [Security Controls](Security_Controls.md).

## 6. Implementation and Validation

The network was configured and tested in Cisco Packet Tracer.

Validation included WAN connectivity, OSPF neighbor formation, inter-VLAN communication, ACL enforcement, switch port security, and administrative access.

Verification procedures and test results are documented in [Validation and Testing](Validation_and_Testing.md).
