---
description: Page contenant des exemples de commande lié au CLI de Cisco
---

# ⌨️ CLI

## CheatSheet

### Configurer un VLAN

```bash
Switch(config)#vlan 2
Switch(config-vlan)#name XXXX
Switch(config-vlan)#ex
```

#### Affectation d'un port à un vlan

```bash
Switch(config)#interface range fastEthernet 0/2-10
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 10
Switch(config-if)#ex
Switch(config)#
```

#### Configuration d'un port en mode trunk

```bash
Switch(config)#interface fastEthernet 0/1
Switch(config-if)#switchport mode trunk
Switch(config-if)#ex
```

#### Pas de recherche DNS

```bash
Switch(config)#no ip domain-lookup
```

#### Configurer le VLAN de gestion

```bash
Switch(config)#vlan 99
Switch(config-vlan)#name Gestion
Switch(config-vlan)#ex
Switch(config)#interface vlan 99
Switch(config-if)#ip address 10.1.99.2 255.255.255.0
Switch(config-if)#ex
```

### Configurer SSH local

```bash
Switch(config)#line vty 0 4
Switch(config)#transport input ssh
Switch(config)#login local
```

### Configuration Router on a Stick

```bash
R1(config)#interface fa0/0.10
R1(config-subif)#encapsulattion dot1q 10
R1(config-subif)#ip address 10.1.10.1 255.255.255.0

R1(config)#interface fa0/0.20
R1(config-subif)#encapsulattion dot1q 20
R1(config-subif)#ip address 10.1.20.1 255.255.255.0

R1(config)#interface fa0/0.30
R1(config-subif)#encapsulattion dot1q 30
R1(config-subif)#ip address 10.1.30.1 255.255.255.0

R1(config)#interface fa0/0.99
R1(config-subif)#encapsulattion dot1q 99
R1(config-subif)#ip address 10.1.99.1 255.255.255.0
```

### Configurer DHCP Client

```bash
R1(config)#interface fa0/1
R1(config-if)#ip address dhcp
R1(config-if)#no shutdown
```

#### Configurer Serveur DHCP IPV4

```bash
R1(config)#ip dhcp pool VLAN10_IPV4
R1(dhcp-config)#network 10.1.10.0 255.255.255.0
R1(config)#ip dhcp pool VLAN20_IPV4
R1(dhcp-config)#network 10.1.20.0 255.255.255.0
```

#### Exclure des address

```bash
R1(config)#ip dhcp excluded-address 10.1.10.1
R1(config)#ip dhcp excluded-address 10.1.20.1
```

#### Attribuer une adresse ipv6 a une interface

```bash
R1(config)#interface fa0/0.30
R1(config)#ipv6 address fc00:beef:000f:130::1/64
R1(config)#ipv6 enable
```

#### Création de DHCPv6

```bash
R1(config)#ipv6 unicast-routing
R1(config)#ipv6 general-prefix IPV6_VLAN20 FC00:BEEF:F:120::/64
R1(config)#ipv6 dhcp pool IPV6_VLAN20
R1(config-dhcpv6)#prefix-delegation pool IPV6_VLAN20
R1(config-dhcpv6)#exit
R1(config)#ipv6 local pool IPV6_VLAN20 fc00:beef:000f:120::/64 64
R1(config)#interface fastEthernet 0/0.20
R1(config-subif)#ipv6 dhcp server IPV6_VLAN20
R1(config-subif)#ipv6 address FE80::1 link-local
R1(config-subif)#ipv6 nd managed-config-flag
R1(config)#exit
```

### Configuration IPV6 Acces-List

```bash
R1(config)#ipv6 access-list NOM
R1(config-ipv6-acl)#deny icmp FC00:BEEF:F:120::/64 FC00:BEEF:F:130::/64
------------------------------------------------------------------------------
R1(config)#interface fa0/0.20
R1(config-subinf)#ipv6 traffic-filter NOM in
```

### Configuration IPV4 Access-List standard

```bash
R1(config)#access-list 20 deny 10.1.10.0 0.0.0.255
R1(config)#access-list 20 permit any
------------------------------------------------------------------------------
R1(config)#interface fa0/0.20
R1(config-subif)#ip access-group 20 in
```

### Configuration IPV4 Access-List Étendue

```bash
R1(config)#access-list 121 deny tcp 10.1.0.0 0.0.255.255 eq ftp any
R1(config)#interface fa0/1
Router(config-if)#ip access-group 121 out
```
