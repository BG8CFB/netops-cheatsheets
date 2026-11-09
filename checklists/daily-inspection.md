# 日常巡检清单（30 项）

> 每日开机后 15 分钟完成。配合 [netcfg-vault](https://github.com/BG8CFB/netcfg-vault) 自动备份配置基线，巡检完一键 diff 出全网变更。

## 电源/环境
- [ ] 设备指示灯无红/橙告警
- [ ] 机房温湿度在阈值内
- [ ] UPS 电量 > 80%

## 设备状态
- [ ] CPU 利用率 < 60%（H3C: display cpu-usage / 华为: display cpu-usage / 思科: show processes cpu）
- [ ] 内存利用率 < 70%
- [ ] 无 active 告警（华为 display alarm active）
- [ ] 风板/电源模块在位
- [ ] 堆叠/IRF/VSS 状态正常（双主控）

## 链路
- [ ] 核心间聚合口全部 Up（无单根链路Down）
- [ ] 上联口无 CRC/错包增长（display interface | include error）
- [ ] 无 flapping 日志
- [ ] 备份链路/WAN 备线状态符合预期

## 二层
- [ ] MAC 表规模无异常暴涨
- [ ] STP 拓扑无变化（display stp brief 对照昨日）
- [ ] 无未知单播泛洪告警

## 三层
- [ ] 核心路由表条目数与基线一致
- [ ] 关键 ping 探测（网关/出口/DNS）通
- [ ] ARP 无异常（display arp | include Incomplete）

## 业务面
- [ ] 出口带宽峰值 < 80%
- [ ] VPN/专线状态 Up
- [ ] DHCP 地址池余量 > 20%
- [ ] 无认证系统异常登录告警

## 变更与备份
- [ ] 昨夜无未报备变更（netcfg-vault diff 一键核对）
- [ ] 当日配置备份成功落盘
- [ ] 备份文件可解密打开（vault list 抽查）

## 记录
- [ ] 异常项已登记工单
- [ ] 巡检报告已发送（用 inspection-report.xlsx 模板）
