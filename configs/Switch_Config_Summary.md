
# Cisco Switch Configurations

Office 1 VLAN segmentation, 802.1Q trunking, and switch port security.

## VLAN Addressing

| VLAN | Name | Network | Gateway |
|---|---|---|---|
| 10 | Management | 172.16.10.160/27 | 172.16.10.161 |
| 20 | Marketing | 172.16.10.192/27 | 172.16.10.193 |
| 30 | Accounting | 172.16.10.224/27 | 172.16.10.225 |
| 100 | Native | — | — |

## S1-Office1

### VLAN Creation

```cisco
enable
configure terminal
hostname S1-Office1

vlan 10
 name Management
vlan 20
 name Marketing
vlan 30
 name Accounting
vlan 100
 name Native
```

### Access Port Configuration

```cisco
interface range FastEthernet0/1-10
 switchport mode access
 switchport access vlan 10
 switchport nonegotiate

interface range FastEthernet0/11-20
 switchport mode access
 switchport access vlan 20
 switchport nonegotiate

interface range FastEthernet0/21-24
 switchport mode access
 switchport access vlan 30
 switchport nonegotiate
```

### Trunk Configuration

Gi0/1 connects to R1; Gi0/2 connects to S2.

```cisco
interface range GigabitEthernet0/1-2
 switchport mode trunk
 switchport trunk native vlan 100
 switchport trunk allowed vlan 10,20,30,100
```

## S2-Office1

### VLAN Creation

```cisco
enable
configure terminal
hostname S2-Office1

vlan 10
 name Management
vlan 20
 name Marketing
vlan 30
 name Accounting
vlan 100
 name Native
```

### Access Port Configuration

```cisco
interface range FastEthernet0/1-10
 switchport mode access
 switchport access vlan 10
 switchport nonegotiate

interface range FastEthernet0/11-20
 switchport mode access
 switchport access vlan 20
 switchport nonegotiate

interface range FastEthernet0/21-24
 switchport mode access
 switchport access vlan 30
 switchport nonegotiate
```

### Trunk Configuration

Gi0/1 connects to S1.

```cisco
interface GigabitEthernet0/1
 switchport mode trunk
 switchport trunk native vlan 100
 switchport trunk allowed vlan 10,20,30,100
```

## Port Security — Both Switches

Apply only to connected end-device access ports, not trunks. The topology identifies Fa0/1, Fa0/11, and Fa0/21 on each switch.

```cisco
interface range FastEthernet0/1, FastEthernet0/11, FastEthernet0/21
 switchport mode access
 switchport port-security
 switchport port-security violation restrict
 switchport port-security mac-address sticky
```

Optional single-device MAC limit:

```cisco
interface range FastEthernet0/1, FastEthernet0/11, FastEthernet0/21
 switchport port-security maximum 1
```

The assignment does not require a specific maximum MAC count. The optional setting is not a verified original configuration.

## Disable Unused Ports

Apply only to verified unused interfaces.

```cisco
interface FastEthernet0/24
 description UNUSED
 shutdown
```

`FastEthernet0/24` is an example; confirm the unused ports before applying.

## Switch Security — Both Switches

Lab credentials only; not intended for production.

```cisco
configure terminal
username Admin password ACDC1973
enable password beatles1960
service password-encryption
banner motd ^COnly authorized personnel are allowed accessing this device!^C

line console 0
 login local

end
copy running-config startup-config
```

## Verification

```cisco
show vlan brief
show interfaces trunk
show interfaces FastEthernet0/1 switchport
show port-security
show port-security address
show port-security interface FastEthernet0/1
show running-config
show startup-config
```

### Inter-VLAN Connectivity

From CEO1:

```text
ping 172.16.10.222
ping 172.16.10.254
```

Expected: successful communication with Copywriter1 and Dialer1 through R1.

> Configuration reference reconstructed from project documentation and topology; not a complete exported running configuration.

