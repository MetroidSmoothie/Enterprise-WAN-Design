
# Cisco Router Configurations

Three-router enterprise WAN using Cisco IOS, OSPF Area 0, and router-on-a-stick inter-VLAN routing.

All networks use `/27` (`255.255.255.224`).

## R1 — Office 1

### Interface Configuration

```cisco
enable
configure terminal
hostname R1

interface GigabitEthernet0/0
 no ip address
 no shutdown

interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 172.16.10.161 255.255.255.224

interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 172.16.10.193 255.255.255.224

interface GigabitEthernet0/0.30
 encapsulation dot1Q 30
 ip address 172.16.10.225 255.255.255.224

interface Serial0/0/1
 ip address 172.16.10.65 255.255.255.224
 no shutdown

interface Serial0/0/0
 ip address 172.16.10.97 255.255.255.224
 no shutdown
```

### OSPF

```cisco
router ospf 1
 router-id 1.1.1.1
 network 172.16.10.64 0.0.0.31 area 0
 network 172.16.10.96 0.0.0.31 area 0
 network 172.16.10.160 0.0.0.31 area 0
 network 172.16.10.192 0.0.0.31 area 0
 network 172.16.10.224 0.0.0.31 area 0
 passive-interface GigabitEthernet0/0.10
 passive-interface GigabitEthernet0/0.20
 passive-interface GigabitEthernet0/0.30
```

## R2 — WAN Transit Router

### Interface Configuration

```cisco
enable
configure terminal
hostname R2

interface Serial0/0/1
 ip address 172.16.10.66 255.255.255.224
 no shutdown

interface Serial0/0/0
 ip address 172.16.10.130 255.255.255.224
 no shutdown
```

### OSPF

```cisco
router ospf 1
 router-id 2.2.2.2
 network 172.16.10.64 0.0.0.31 area 0
 network 172.16.10.128 0.0.0.31 area 0
```

## R3 — Office 2 and Office 3

### Interface Configuration

```cisco
enable
configure terminal
hostname R3

interface GigabitEthernet0/0
 ip address 172.16.10.1 255.255.255.224
 no shutdown

interface GigabitEthernet0/1
 ip address 172.16.10.33 255.255.255.224
 no shutdown

interface Serial0/0/0
 ip address 172.16.10.98 255.255.255.224
 no shutdown

interface Serial0/0/1
 ip address 172.16.10.129 255.255.255.224
 no shutdown
```

### OSPF

```cisco
router ospf 1
 router-id 3.3.3.3
 network 172.16.10.0 0.0.0.31 area 0
 network 172.16.10.32 0.0.0.31 area 0
 network 172.16.10.96 0.0.0.31 area 0
 network 172.16.10.128 0.0.0.31 area 0
 passive-interface GigabitEthernet0/0
 passive-interface GigabitEthernet0/1
```

### Extended ACL — Guest Isolation

Blocks Guest PC `172.16.10.60` from NTP/Syslog server `172.16.10.29`, permitting all other traffic.

```cisco
access-list 100 deny ip host 172.16.10.60 host 172.16.10.29
access-list 100 permit ip any any

interface GigabitEthernet0/1
 ip access-group 100 in
```

Verified using `show access-lists` and `show ip interface GigabitEthernet0/1`.

## Router Security — Apply to R1, R2, R3

Lab credentials only; not intended for production.

```cisco
configure terminal
username Admin password ACDC1973
enable password beatles1960
service password-encryption
banner motd ^COnly authorized personnel are allowed accessing this device!^C

ip domain-name Cyber.local
crypto key generate rsa modulus 1024
ip ssh version 2

line console 0
 login local

line vty 0 4
 login local
 transport input ssh

line vty 5 15
 login local
 transport input ssh

end
copy running-config startup-config
```

Omit `line vty 5 15` on devices that do not support that range.

## Verification

```cisco
show ip interface brief
show ip ospf neighbor
show ip route
show ip protocols
show access-lists
show ip ssh
show startup-config
```

On R3:

```cisco
show ip interface GigabitEthernet0/1
```

Expected: `Inbound access list is 100`.

> Configuration reference reconstructed from project documentation and verified corrections; not a complete exported running configuration.

