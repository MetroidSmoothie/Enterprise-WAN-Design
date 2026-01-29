# IP Addressing Plan — Enterprise WAN (Mock Bank)

## Overview
This project uses the **172.16.10.0/24** address space. The /24 was subnetted into **8 equal subnets** to support:
- Office 3 LAN
- Office 2 LAN
- Three WAN subnets (router-to-router connectivity)
- Office 1 segmented into three VLANs (CEO / Copywriter / Dialer)

**Gateway convention:** the first usable IP in each LAN/VLAN subnet is reserved as the default gateway (router interface/subinterface).

---

## Subnetting Summary
- **Base network:** 172.16.10.0/24  
- **Subnet mask:** 255.255.255.224 (**/27**)  
- **Number of subnets:** 8  
- **Usable hosts per subnet:** 30  

---

## Subnet Allocation

| Subnet | Purpose / Site | Network (CIDR) | Default Gateway | Usable Host Range | Broadcast |
|------:|-----------------|----------------|-----------------|------------------|----------|
| 1 | Office 3 LAN | 172.16.10.0/27 | 172.16.10.1 | 172.16.10.1 – 172.16.10.30 | 172.16.10.31 |
| 2 | Office 2 LAN | 172.16.10.32/27 | 172.16.10.33 | 172.16.10.33 – 172.16.10.62 | 172.16.10.63 |
| 3 | WAN Subnet (Router Link) | 172.16.10.64/27 | N/A | 172.16.10.65 – 172.16.10.94 | 172.16.10.95 |
| 4 | WAN Subnet (Router Link) | 172.16.10.96/27 | N/A | 172.16.10.97 – 172.16.10.126 | 172.16.10.127 |
| 5 | WAN Subnet (Router Link) | 172.16.10.128/27 | N/A | 172.16.10.129 – 172.16.10.158 | 172.16.10.159 |
| 6 | Office 1 VLAN 10 — CEO | 172.16.10.160/27 | 172.16.10.161 | 172.16.10.161 – 172.16.10.190 | 172.16.10.191 |
| 7 | Office 1 VLAN 20 — Copywriter | 172.16.10.192/27 | 172.16.10.193 | 172.16.10.193 – 172.16.10.222 | 172.16.10.223 |
| 8 | Office 1 VLAN 30 — Dialer | 172.16.10.224/27 | 172.16.10.225 | 172.16.10.225 – 172.16.10.254 | 172.16.10.255 |

---

## Site Addressing Details

### Office 3 LAN (Subnet 1 — 172.16.10.0/27)
**Default gateway:** 172.16.10.1

| Device | IP Address |
|--------|------------|
| Email Server | 172.16.10.30 |
| Syslog / NTP Server | 172.16.10.29 |
| Admin Workstation | 172.16.10.28 |

---

### Office 2 LAN (Subnet 2 — 172.16.10.32/27)
**Default gateway:** 172.16.10.33

| Device | IP Address |
|--------|------------|
| Employee1 | 172.16.10.62 |
| Employee2 | 172.16.10.61 |
| Guest | 172.16.10.60 |

---

## Office 1 VLANs (Router-on-a-Stick)

### VLAN 10 — CEO (Subnet 6 — 172.16.10.160/27)
**Default gateway:** 172.16.10.161

| Device | IP Address |
|--------|------------|
| CEO1 | 172.16.10.190 |
| CEO2 | 172.16.10.189 |

---

### VLAN 20 — Copywriter (Subnet 7 — 172.16.10.192/27)
**Default gateway:** 172.16.10.193

| Device | IP Address |
|--------|------------|
| Copywriter1 | 172.16.10.222 |
| Copywriter2 | 172.16.10.221 |

> Note: In a /27, **172.16.10.223 is the broadcast address** for this subnet, so Copywriter2 must use an address in the usable range (**172.16.10.193–172.16.10.222**). This plan assigns Copywriter2 **172.16.10.221**.

---

### VLAN 30 — Dialer (Subnet 8 — 172.16.10.224/27)
**Default gateway:** 172.16.10.225

| Device | IP Address |
|--------|------------|
| Dialer1 | 172.16.10.254 |
| Dialer2 | 172.16.10.253 |

---

## Addressing Standards & Notes
- **Gateways** use the first usable IP in each LAN/VLAN subnet.
- **Infrastructure interfaces** (routers/switch management) use static IPs.
- **Endpoints** are assigned within their subnet’s usable range.
- WAN subnets are documented as router-to-router networks (no gateway concept).

