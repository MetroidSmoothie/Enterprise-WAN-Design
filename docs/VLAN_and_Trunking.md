
# VLANs & Trunking

## Overview

Office 1 uses three VLANs across two Cisco switches to separate departmental broadcast domains. IEEE 802.1Q trunking carries VLAN traffic between switches and R1, which provides inter-VLAN routing.

## VLAN Configuration

| VLAN | Name | Network | Default Gateway |
|---|---|---|---|
| 10 | Management | `172.16.10.160/27` | `172.16.10.161` |
| 20 | Marketing | `172.16.10.192/27` | `172.16.10.193` |
| 30 | Accounting | `172.16.10.224/27` | `172.16.10.225` |

VLANs are configured on both S1-Office1 and S2-Office1.

## Trunk Connections

| Device | Interface | Connection | Mode |
|---|---|---|---|
| S1-Office1 | Gi0/1 | R1 Gi0/0 | 802.1Q trunk |
| S1-Office1 | Gi0/2 | S2-Office1 | 802.1Q trunk |
| S2-Office1 | Gi0/1 | S1-Office1 | 802.1Q trunk |

Trunks carry VLANs 10, 20, and 30.

## Inter-VLAN Routing

R1 uses router-on-a-stick with one subinterface per VLAN.

```cisco
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 172.16.10.161 255.255.255.224

interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 172.16.10.193 255.255.255.224

interface GigabitEthernet0/0.30
 encapsulation dot1Q 30
 ip address 172.16.10.225 255.255.255.224
```

Each subinterface acts as the default gateway for its corresponding VLAN.

## Verification

```cisco
show vlan brief
show interfaces trunk
show interfaces switchport
```

On R1:

```cisco
show ip interface brief
show ip route connected
```

Inter-VLAN connectivity can be tested from CEO1 to:

```text
ping 172.16.10.222
ping 172.16.10.254
```

These addresses correspond to Copywriter1 (VLAN 20) and Dialer1 (VLAN 30).

## Related Documentation

- [IP Addressing Plan](IP_Addressing_Plan.md)
- [Router Configurations](../configs/Router_Configuration.md)
- [Switch Configurations](../configs/Switch_Configuration.md)
- [Validation & Testing](Validation_and_Testing.md)
