# Routing and OSPF

---

## Overview

This document describes the routing implementation used to provide end-to-end connectivity between all LANs and VLANs across the WAN.

Addressing details and network design decisions are documented separately in:

- Network_Design_Document.md
- IP_Addressing_Plan.md

This file focuses only on routing behavior, configuration approach, and validation.

---

## Routing Architecture

### Inter-VLAN Routing (Office 1)
Office 1 uses **Router-on-a-Stick** to enable communication between VLANs.

- 802.1Q trunk between switch and router
- Router subinterfaces provide default gateways
- Each VLAN routed locally at the branch gateway

This approach centralizes Layer 3 routing while keeping switching at Layer 2.

---

### WAN Routing Protocol

### Protocol: OSPF (Area 0)

OSPF is used between all routers to dynamically advertise networks and maintain routing tables.

OSPF was selected because it:

- Eliminates manual static routes
- Automatically propagates new networks
- Provides fast convergence
- Scales better for multi-site environments
- Reflects common enterprise routing practice

All routers participate in a single backbone area (Area 0).

---

## Route Advertisement Strategy

Each router advertises:

- Its directly connected LAN or VLAN networks
- Its WAN interfaces

Best practices applied:

- Passive interfaces on LAN segments
- OSPF enabled only on required interfaces
- Stable router IDs for predictable neighbor relationships

---

## Traffic Flow Summary

### Local VLAN traffic
- Routed by the branch router via subinterfaces

### Inter-office traffic
- Routed across WAN links
- Learned dynamically through OSPF

### Guest/Restricted traffic
- Forwarded normally by routing
- Controlled by ACL policies (see Security documentation)

---

## Verification Commands

The following commands were used to confirm proper routing behavior:

### OSPF neighbors
Confirm adjacency between routers:
- show ip ospf neighbor

Expected: FULL state with all neighboring routers

---

### Routing table
Confirm remote networks are learned:
- show ip route

Expected: remote subnets appear as OSPF-learned routes

---

### Interface status
Verify interfaces are operational:
- show ip interface brief

Expected: all routed interfaces up/up

---

### End-to-end testing
- ping between VLANs
- ping between offices
- traceroute to confirm correct path selection

Expected: successful connectivity across all segments

---

## Troubleshooting Notes

Common issues and resolutions:

### No OSPF neighbors
- Check interface status
- Verify both sides are in the same area
- Confirm correct network statements

### Routes missing
- Confirm networks are advertised into OSPF
- Check passive-interface configuration

### Inter-VLAN communication failing
- Verify trunk configuration
- Confirm subinterface encapsulation
- Confirm default gateway settings

---

## Skills Demonstrated

- Dynamic routing with OSPF
- Router-on-a-Stick inter-VLAN routing
- Route verification and troubleshooting
- Enterprise-style routing design and validation

