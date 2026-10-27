
# Validation & Testing

## Overview

Network functionality was manually validated in Cisco Packet Tracer using connectivity tests, IOS verification commands, and security control testing.

## 1. Connectivity Tests 8/8 PASS

| Source | Destination | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| CEO1 | Copywriter1 (`172.16.10.222`) | Reachable | Reachable | PASS |
| CEO1 | Dialer1 (`172.16.10.254`) | Reachable | Reachable | PASS |
| Admin PC | CEO1 (`172.16.10.190`) | Reachable | Reachable | PASS |
| Admin PC | Employee1 (`172.16.10.62`) | Reachable | Reachable | PASS |
| Employee2 | Copywriter1 (`172.16.10.222`) | Reachable | Reachable | PASS |
| Employee2 | Dialer1 (`172.16.10.254`) | Reachable | Reachable | PASS |
| Guest (`172.16.10.60`) | NTP/Syslog (`172.16.10.29`) | Blocked | Blocked | PASS |
| Guest (`172.16.10.60`) | Email Server (`172.16.10.30`) | Reachable | Reachable | PASS |

## 2. Routing Verification

Verification commands:

```cisco
show ip interface brief
show ip ospf neighbor
show ip route
show ip protocols
```

| Router | Expected OSPF Neighbors |
|---|---|
| R1 | R2, R3 |
| R2 | R1, R3 |
| R3 | R1, R2 |

## 3. VLAN & Switch Verification

Verification commands:

```cisco
show vlan brief
show interfaces trunk
show port-security
show port-security address
show port-security interface FastEthernet0/1
```

Validation covers VLAN membership, trunk operation, sticky MAC learning, and port-security configuration.

## 4. ACL Verification

ACL 100 was verified inbound on R3 GigabitEthernet0/1.

| Check | Observed Result | Status |
|---|---|---|
| ACL 100 configured | Confirmed | PASS |
| Inbound application on Gi0/1 | Confirmed | PASS |
| Guest-to-NTP/Syslog restriction | Blocked | PASS |
| Other traffic permitted | Confirmed | PASS |

Observed ACL counters:

- Deny entry: 16 matches
- Permit entry: 19 matches

## 5. Management Access Verification

```cisco
show ip ssh
show running-config
```

Management configuration includes SSHv2, local authentication, and SSH-only VTY access on routers.

## 6. Configuration Persistence

```cisco
show startup-config
```

Configurations were saved to NVRAM using:

```cisco
copy running-config startup-config
```

## Related Documentation

- [Network Design](Network_Design_Document.md)
- [Routing & OSPF](Routing_and_OSPF.md)
- [Security Controls](Security_Controls.md)
- [Router Configurations](../configs/Router_Configuration.md)
- [Switch Configurations](../configs/Switch_Configuration.md)
