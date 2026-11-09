# 思科 IOS 常用配置速查

## 基础

```bash
configure terminal
hostname CORE-SW1
show version
show running-config
copy running-config startup-config    # 或 write memory
```

## VLAN

```bash
vlan 100
 name OFFICE
interface Vlan100
 ip address 192.168.100.1 255.255.255.0

interface range GigabitEthernet1/0/1 - 10
 switchport mode access
 switchport access vlan 100

interface GigabitEthernet1/0/24
 switchport trunk encapsulation dot1q    # 3560 等需先设
 switchport mode trunk
 switchport trunk allowed vlan 100,200
```

## EtherChannel

```bash
interface range GigabitEthernet1/0/1 - 2
 channel-group 1 mode active        # LACP
interface Port-channel1
 switchport mode trunk
```

## AAA + SSH

```bash
username admin privilege 15 secret <PWD>
ip domain-name corp.local
crypto key generate rsa modulus 2048
line vty 0 4
 transport input ssh
 login local
aaa new-model
```

## NTP / SNMP

```bash
ntp server 192.168.1.10
snmp-server community <RO> RO
snmp-server host 192.168.1.20 version 2c <RO>
```

## 端口安全

```bash
interface GigabitEthernet1/0/5
 switchport port-security
 switchport port-security maximum 4
 switchport port-security violation restrict
 switchport port-security mac-address sticky
```

## 排障

```bash
show interfaces status
show etherchannel summary
show spanning-tree
show mac address-table
show ip arp
show ip route
show processes cpu sorted
show logging
```
