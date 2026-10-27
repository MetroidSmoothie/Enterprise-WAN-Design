
# Routing & OSPF

## Overview

Three Cisco routers form a triangular WAN topology connecting Office 1, Office 2, and Office 3. OSPF process 1, Area 0 provides dynamic routing between the sites.

## WAN Connections

| Link | Network | R1 | R2 | R3 |
|---|---|---|---|---|
| R1–R2 | `172.16.10.64/27` | `.65` | `.66` | — |
| R1–R3 | `172.16.10.96/27` | `.97` | — | `.98` |
| R2–R3 | `172.16.10.128/27` | — | `.130` | `.129` |

*Abbreviated addresses use the `172.16.10.x` prefix.*

## OSPF Design

| Router | Router ID | Advertised Networks | Passive Interfaces |
|---|---|---|---|
| R1 | `1.1.1.1` | R1–R2, R1–R3, VLANs 10/20/30 | Gi0/0.10, Gi0/0.20, Gi0/0.30 |
| R2 | `2.2.2.2` | R1–R2, R2–R3 | None |
| R3 | `3.3.3.3` | R1–R3, R2–R3, Office 2, Office 3 | Gi0/0, Gi0/1 |

Passive interfaces advertise connected LAN networks without forming OSPF neighbor relationships on those interfaces.

## Expected OSPF Adjacencies

| Router | Expected Neighbors |
|---|---|
| R1 | R2, R3 |
| R2 | R1, R3 |
| R3 | R1, R2 |

The triangular topology provides an alternate WAN path if a direct link becomes unavailable, subject to routing convergence.

## Implementation & Testing

- [Router Configurations](../configs/Router_Configuration.md)
- [IP Addressing Plan](IP_Addressing_Plan.md)
- [Validation & Testing](Validation_and_Testing.md)
