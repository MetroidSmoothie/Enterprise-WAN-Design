
# IP Addressing Plan

## Addressing Summary

| Parameter | Value |
|---|---|
| Base Network | `172.16.10.0/24` |
| Subnet Mask | `255.255.255.224` (`/27`) |
| Subnets | 8 equal-sized networks |
| Usable Hosts | 30 per subnet |
| Gateway Convention | First usable IP in each LAN/VLAN |

## Subnet Allocation

| Office / Purpose | VLAN | Network | Gateway | Usable Range | Broadcast |
|---|---|---|---|---|---|
| Office 3 | — | `172.16.10.0/27` | `.1` | `.1–.30` | `.31` |
| Office 2 | — | `172.16.10.32/27` | `.33` | `.33–.62` | `.63` |
| R1–R2 WAN | — | `172.16.10.64/27` | — | `.65–.94` | `.95` |
| R1–R3 WAN | — | `172.16.10.96/27` | — | `.97–.126` | `.127` |
| R2–R3 WAN | — | `172.16.10.128/27` | — | `.129–.158` | `.159` |
| Office 1 — Management | 10 | `172.16.10.160/27` | `.161` | `.161–.190` | `.191` |
| Office 1 — Marketing | 20 | `172.16.10.192/27` | `.193` | `.193–.222` | `.223` |
| Office 1 — Accounting | 30 | `172.16.10.224/27` | `.225` | `.225–.254` | `.255` |

*Abbreviated addresses use the `172.16.10.x` prefix.*

## Router Interface Addressing

| Router | Interface | IP Address | Network |
|---|---|---|---|
| R1 | Gi0/0.10 | `172.16.10.161/27` | Office 1 — VLAN 10 |
| R1 | Gi0/0.20 | `172.16.10.193/27` | Office 1 — VLAN 20 |
| R1 | Gi0/0.30 | `172.16.10.225/27` | Office 1 — VLAN 30 |
| R1 | S0/0/1 | `172.16.10.65/27` | R1–R2 |
| R1 | S0/0/0 | `172.16.10.97/27` | R1–R3 |
| R2 | S0/0/1 | `172.16.10.66/27` | R1–R2 |
| R2 | S0/0/0 | `172.16.10.130/27` | R2–R3 |
| R3 | Gi0/0 | `172.16.10.1/27` | Office 3 |
| R3 | Gi0/1 | `172.16.10.33/27` | Office 2 |
| R3 | S0/0/0 | `172.16.10.98/27` | R1–R3 |
| R3 | S0/0/1 | `172.16.10.129/27` | R2–R3 |

## Endpoint Addressing

| Office / VLAN | Device | IP Address |
|---|---|---|
| Office 3 | Email Server | `172.16.10.30` |
| Office 3 | NTP/Syslog Server | `172.16.10.29` |
| Office 3 | Admin Workstation | `172.16.10.28` |
| Office 2 | Employee1 | `172.16.10.62` |
| Office 2 | Employee2 | `172.16.10.61` |
| Office 2 | Guest | `172.16.10.60` |
| Office 1 — VLAN 10 | CEO1 | `172.16.10.190` |
| Office 1 — VLAN 10 | CEO2 | `172.16.10.189` |
| Office 1 — VLAN 20 | Copywriter1 | `172.16.10.222` |
| Office 1 — VLAN 20 | Copywriter2 | `172.16.10.221` |
| Office 1 — VLAN 30 | Dialer1 | `172.16.10.254` |
| Office 1 — VLAN 30 | Dialer2 | `172.16.10.253` |

All listed interfaces and endpoints use subnet mask `255.255.255.224`.
