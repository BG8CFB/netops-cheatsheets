# 华为 VRP 常用配置速查

适用 VRP V200（S 系列 CE/交换机为主）。

## 基础

```bash
system-view
sysname ACC-SW1
display version
display current-configuration
display saved-configuration
save                                    # 保存（y 确认）
```

## VLAN

```bash
vlan batch 100 200                      # 批量建
interface Vlanif100
ip address 192.168.100.1 24
quit

interface GigabitEthernet0/0/24
port link-type trunk
port trunk allow-pass vlan 100 200

# 批量 access 口
port-group group-member GigabitEthernet0/0/1 to GigabitEthernet0/0/10
port link-type access
port default vlan 100
```

## 堆叠 (iStack)

```bash
stack slot 0 priority 100               # 主
interface stack-port 0/1
port interface GigabitEthernet0/0/49 enable
# 从机改 slot 1 后重启
display stack
```

## MSTP

```bash
stp mode mstp
stp region-configuration
region-name RG1
instance 1 vlan 100
instance 2 vlan 200
active region-configuration
quit
stp root primary
```

## SSH

```bash
rsa local-key-pair create
stelnet server enable
ssh user admin
ssh user admin authentication-type password
ssh user admin service-type stelnet
user-interface vty 0 4
authentication-mode aaa
protocol inbound ssh
quit
aaa
local-user admin password irreversible-cipher <PWD>
local-user admin privilege level 15
local-user admin service-type ssh
```

## NTP / 告警

```bash
ntp-service unicast-peer 192.168.1.10
info-center loghost 192.168.1.20
snmp-agent
snmp-agent community read cipher <SNMPV2C>
snmp-agent target-host trap address udp-domain 192.168.1.20 params securityname <SNMPV2C>
```

## 排障

```bash
display interface brief
display eth-trunk
display stp brief
display mac-address
display arp all
display ip routing-table
display alarm active                 # 当前告警
display logbuffer                    # 日志缓冲
```
