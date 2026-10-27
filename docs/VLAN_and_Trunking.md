
# VLANs & Trunking

## Overview

Office 1 uses three VLANs across two Cisco switches to separate departmental broadcast domains. IEEE 802.1Q trunking carries VLAN traffic between switches and R1, which provides inter-VLAN routing.

## VLAN Design

| VLAN | Department | Subnet | Default Gateway |
|---|---|---|---|
| 10 | Management | `172.16.10.160/27` | `172.16.10.161` |
| 20 | Marketing | `172.16.10.192/27` | `172.16.10.193` |
| 30 | Accounting | `172.16.10.224/27` | `172.16.10.225` |

VLANs are configured on both S1-Office1 and S2-Office1.

## Trunk Connections

| Device | Interface | Connected Device | Mode |
|---|---|---|---|
| S1-Office1 | Gi0/1 | R1 Gi0/0 | 802.1Q Trunk |
| S1-Office1 | Gi0/2 | S2-Office1 | 802.1Q Trunk |
| S2-Office1 | Gi0/1 | S1-Office1 | 802.1Q Trunk |

Trunk links carry VLANs 10, 20, and 30 between switches and the router.

## Inter-VLAN Routing

R1 uses router-on-a-stick to route traffic between Office 1 VLANs through subinterfaces on GigabitEthernet0/0.

| Subinterface | VLAN | Gateway |
|---|---|---|
| Gi0/0.10 | 10 | `172.16.10.161` |
| Gi0/0.20 | 20 | `172.16.10.193` |
| Gi0/0.30 | 30 | `172.16.10.225` |

Each VLAN operates as a separate broadcast domain. Inter-VLAN communication is permitted through R1 unless restricted by an applicable access control policy.
