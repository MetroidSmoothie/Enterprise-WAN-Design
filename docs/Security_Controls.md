
# Network Security Controls

## Overview

The enterprise WAN implements network access restrictions, switch port security, and device management controls using Cisco IOS.

## 1. Extended Access Control List (ACL)

A numbered extended ACL restricts traffic from the Office 2 Guest workstation to the Office 3 NTP/Syslog server.

| Parameter | Configuration |
|---|---|
| Device | R3 |
| ACL | 100 (Extended) |
| Interface | GigabitEthernet0/1 |
| Direction | Inbound |
| Source | Guest — `172.16.10.60` |
| Destination | NTP/Syslog — `172.16.10.29` |
| Action | Deny IP traffic |
| Other Traffic | Explicitly permitted |

**Verification:** `show access-lists` confirmed matches on both the deny and permit entries. `show ip interface GigabitEthernet0/1` confirmed ACL 100 applied inbound.

## 2. Switch Port Security

Port security is configured on Office 1 end-device access ports to control which MAC addresses can use those interfaces.

| Control | Implementation |
|---|---|
| Devices | S1-Office1, S2-Office1 |
| Interfaces | End-device access ports |
| MAC Learning | Sticky |
| Violation Mode | Restrict |
| Trunk Interfaces | Excluded |
| Unused Interfaces | Administratively disabled |

Sticky MAC learning records dynamically learned MAC addresses in the running configuration. Restrict mode drops frames from unauthorized MAC addresses without shutting down the interface.

## 3. Device Authentication & Management

| Control | Implementation |
|---|---|
| Local Authentication | Cisco IOS local user database |
| Console Access | Local login authentication |
| Privileged EXEC | Enable password |
| Remote Router Access | SSH version 2 |
| SSH Authentication | Local credentials |
| VTY Access | SSH-only |
| Login Banner | Authorized-access warning |
| Password Obfuscation | `service password-encryption` |

SSH provides encrypted remote management sessions. Cisco IOS password obfuscation is not equivalent to secure password hashing.

## 4. VLAN Segmentation

Office 1 uses three VLANs to separate departmental broadcast domains.

| VLAN | Department |
|---|---|
| 10 | Management |
| 20 | Marketing |
| 30 | Accounting |

Inter-VLAN routing is enabled through R1. VLAN membership alone does not prevent communication between departments; additional filtering would be required to enforce departmental traffic restrictions.

## Implementation & Testing

- [Router Configurations](../configs/Router_Configuration.md)
- [Switch Configurations](../configs/Switch_Configuration.md)
- [VLANs & Trunking](VLAN_and_Trunking.md)
- [Validation & Testing](Validation_and_Testing.md)
