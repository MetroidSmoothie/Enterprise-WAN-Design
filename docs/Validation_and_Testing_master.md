
# Validation and Testing

---

## Overview

This document provides a complete end-to-end validation checklist used to verify that the enterprise WAN, VLAN segmentation, routing, and security controls are functioning correctly after implementation.

The goal is to systematically confirm:

- Physical connectivity
- VLAN segmentation
- Inter-VLAN routing
- WAN routing (OSPF)
- End-to-end reachability
- Security enforcement
- Device hardening

This serves as a final acceptance test for the network.

---

## Testing Methodology

Validation follows a layered approach:

1. Layer 1–2 (interfaces, VLANs, trunks)
2. Layer 3 (routing & gateways)
3. WAN connectivity
4. Security controls
5. End-to-end functional testing

Each section builds on the previous one.

---

# Phase 1 — Interface & Device Health

## Objective
Ensure all devices and links are operational.

### Commands
- show ip interface brief
- show interfaces status

### Verify
- All required interfaces are up/up
- No unexpected administratively down ports
- No physical link failures

---

# Phase 2 — VLAN & Switching Validation

## Objective
Confirm correct Layer 2 segmentation.

### Commands
- show vlan brief
- show interfaces trunk

### Verify
- All VLANs exist
- Access ports assigned correctly
- Trunk links active
- Correct VLANs allowed on trunk

### Functional Tests
From each VLAN:
- Ping local host in same VLAN → should succeed
- Attempt direct cross-VLAN ping → should fail without routing

---

# Phase 3 — Default Gateway Validation

## Objective
Confirm hosts can reach their gateway.

### Test (per VLAN/LAN)
- Ping default gateway

### Expected
- Successful reply

Failure here indicates:
- Wrong IP
- Wrong VLAN assignment
- Trunk issue
- Subinterface misconfiguration

---

# Phase 4 — Inter-VLAN Routing Validation

## Objective
Confirm Router-on-a-Stick routing works.

### Tests
From each VLAN:
- Ping host in another VLAN

### Expected
- Successful communication

### Troubleshoot if failed
- Verify trunk
- Verify subinterfaces
- Verify encapsulation
- Verify gateway settings

---

# Phase 5 — OSPF Neighbor Validation

## Objective
Confirm dynamic routing adjacencies.

### Commands
- show ip ospf neighbor

### Expected
- All routers listed
- State = FULL

Failure indicates:
- Area mismatch
- Interface down
- Network statement missing
- Incorrect addressing

---

# Phase 6 — Route Table Validation

## Objective
Ensure all networks are learned dynamically.

### Commands
- show ip route

### Verify
- Remote LAN/VLAN subnets present
- Marked as OSPF-learned routes (O)

### Expected
- No missing routes
- No manual static routes required

---

# Phase 7 — WAN Connectivity Testing

## Objective
Verify inter-site communication.

### Tests
From each office:
- Ping remote office gateway
- Ping remote workstation
- Run traceroute

### Expected
- Successful connectivity
- Logical routing path across WAN routers

---

# Phase 8 — Security Control Validation

## VLAN Isolation
- Confirm devices cannot bypass gateway to reach other VLANs

## ACL Enforcement
- Test restricted traffic (guest → internal)
- Expected: blocked
- Test permitted traffic
- Expected: allowed

## Port Security
- Attempt connecting unauthorized device
- Expected: violation triggered or blocked

## Device Management
- SSH works
- Telnet fails
- Console login required

---

# Phase 9 — End-to-End Scenario Testing

## Objective
Validate full business functionality.

### Example tests
- Office 1 → Office 2 communication
- Office 1 → Office 3 servers
- Office 2 → Office 3 services
- Cross-site resource access

### Expected
- All legitimate traffic succeeds
- No unintended restrictions

---

# Phase 10 — Failure Simulation (Optional but Recommended)

## Objective
Confirm resiliency and troubleshooting capability.

### Tests
- Disable a link
- Restart OSPF neighbor
- Re-enable

### Expected
- Routes reconverge automatically
- Connectivity restored

---

# Acceptance Criteria

The network is considered operational when:

- All interfaces are up
- VLANs function correctly
- Gateways reachable
- Inter-VLAN routing works
- OSPF neighbors established
- All routes present
- Inter-site communication successful
- Security controls enforced
- Management secured via SSH

---

# Skills Demonstrated

- Structured network validation methodology
- Layered troubleshooting
- OSPF verification
- VLAN and trunk validation
- Security testing
- End-to-end connectivity assurance

---

## Notes

Addressing details:
→ IP_Addressing_Plan.md

Architecture:
→ Network_Design_Document.md

Routing behavior:
→ Routing_and_OSPF.md

Security controls:
→ Security_Controls.md
