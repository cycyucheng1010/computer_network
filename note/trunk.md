# Trunk
* Switch和Switch之間

## 實驗一

* SW設定vlan
```
//SW1
sw1(config)#vlan 10
sw1(config-vlan)#name vlan10
sw1(config-vlan)#exit
sw1(config)#vlan 20
sw1(config-vlan)#name vlan20
sw1(config-vlan)#int e0/0
sw1(config-if)#sw mode access
sw1(config-if)#sw access vlan 10
sw1(config-if)#int e0/1
sw1(config-if)#sw mode access
sw1(config-if)#sw access vlan 20
//SW2
sw2(config)#vlan 10
sw2(config-vlan)#name vlan10
sw2(config-vlan)#exit
sw2(config)#vlan 20
sw2(config-vlan)#name vlan20
sw2(config-vlan)#int e0/0
sw2(config-if)#sw mode access
sw2(config-if)#sw access vlan 10
sw2(config-if)#int e0/1
sw2(config-if)#sw mode access
sw2(config-if)#sw access vlan 20
```

*  PC設定IP
```
//PC1
VPC3> ip 192.168.10.1 255.255.255.0
//PC2
VPC4> ip 192.168.20.1 255.255.255.0
//PC3
VPC5> ip 192.168.10.2 255.255.255.0
//PC4
VPC6> ip 192.168.20.2 255.255.255.0
```
*  SW設定trunk
```
//SW1
sw1(config)#int e0/2
sw1(config-if)#switchport trunk encapsulation dot1q       //封裝格式
sw1(config-if)#switchport mode trunk
//SW2
sw2(config)#int e0/2
sw2(config-if)#switchport trunk encapsulation dot1q
sw2(config-if)#switchport mode trunk
sw2(config-if)#do sh interface trunk
```
