# VLANs and Trunking

---

## Overview

This document describes the VLAN segmentation and trunking configuration used to logically separate departments and transport multiple VLANs between switches and routers.

Detailed addressing information is documented separately in:

- Network_Design_Document.md
- IP_Addressing_Plan.md

This file focuses only on VLAN implementation and trunk behavior.

---

## VLAN Strategy

VLANs were implemented to segment traffic by department and function.

Segmentation provides:

- Reduced broadcast domains
- Improved performance
- Logical isolation between groups
- Enhanced security and policy enforcement
- Easier network management

---

## Office 1 VLAN Layout

Office 1 contains multiple departments and was segmented into dedicated VLANs.

| VLAN | Purpose |
|--------|-----------|
| 10 | Executive / CEO |
| 20 | Copywriter Team |
| 30 | Dialer Team |

Each VLAN operates as an independent Layer 2 broadcast domain.

Inter-VLAN communication is handled by the branch router (Router-on-a-Stick).

---

## Access Ports

End-user devices connect through access ports assigned to a single VLAN.

### Behavior
- Port carries traffic for only one VLAN
- Untagged frames
- Simplifies endpoint configuration

### Example configuration tasks
- Assign port to VLAN
- Disable dynamic negotiation if required
- Enable port security (see Security documentation)

---

## Trunking

### Purpose

Trunk links allow multiple VLANs to traverse a single physical connection between:

- Switch ↔ Router
- Switch ↔ Switch

This enables VLAN traffic to reach the routing device for inter-VLAN communication.

---

### Trunk Characteristics

- 802.1Q encapsulation
- Tagged frames
- Carries multiple VLANs simultaneously
- Native VLAN support (if configured)

---

### Trunk Links Implemented

| Connection | Purpose |
|-------------|-------------|
| Switch ↔ Router | Inter-VLAN routing (Router-on-a-Stick) |
| Switch ↔ Switch (if applicable) | VLAN propagation between switches |

---

## Router-on-a-Stick Integration

A trunk link connects the switch to the router.

The router:

- Uses subinterfaces
- Tags traffic per VLAN
- Acts as the default gateway for each VLAN
- Performs inter-VLAN routing

Traffic flow:

Host → Access Port → Switch → Trunk → Router → Destination VLAN

---

## Verification Commands

The following checks were used to confirm VLAN and trunk operation:

### VLAN status
- show vlan brief

Expected:
- VLANs created
- Access ports correctly assigned

---

### Trunk status
- show interfaces trunk

Expected:
- Trunk link active
- Correct encapsulation
- VLANs allowed on trunk

---

### Connectivity tests
- Ping default gateway from each VLAN
- Ping hosts across VLANs

Expected:
- Successful inter-VLAN communication through the router

---

## Common Issues and Fixes

### Devices cannot reach gateway
- Verify correct VLAN assignment
- Confirm access port mode

### VLAN traffic not passing between devices
- Check trunk configuration
- Verify VLAN allowed list

### Inter-VLAN routing not working
- Confirm trunk is up
- Confirm router subinterfaces exist
- Verify encapsulation matches VLAN IDs

---

## Skills Demonstrated

- VLAN segmentation
- Access vs trunk port configuration
- 802.1Q trunking
- Router-on-a-Stick integration
- Broadcast domain reduction
- Layer 2 troubleshooting

