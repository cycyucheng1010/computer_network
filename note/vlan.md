# vlan
* VLAN：Layer 2 的虛擬網路化技術
* 一台交換機預設處在某個區域網路下，當節點數越多，競爭越多，就會影響效能、寬頻、安全性。
* 將主機或servers分組分域，以便於管理。例如：可將公司的不同部門放入不同的VLAN，在默認情況下，不同VLAN之間要通訊，必須透過第三層的網路設備。

## 實驗一

![image](https://user-images.githubusercontent.com/62127656/148352958-dc76f301-3941-49de-aefc-fb1b5f5afb33.png)

設定IP
```
VPC2
>ip 192.168.1.1 255.255.255.0
VPC3
>ip 192.168.1.2 255.255.255.0
VPC4
>ip 192.168.1.3 255.255.255.0
VPC5
>ip 192.168.1.4 255.255.255.0
```
SW設定VLAN
```
Switch(config)#vlan 10
Switch(config-vlan)#name RD
Switch(config-vlan)#exit
Switch(config)#vlan 20
Switch(config-vlan)#name SALES
Switch(config-vlan)#exit
Switch(config)#do sh vlan brief
```
```
Switch(config)#int e0/0
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 10
Switch(config-if)#int e0/1
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 10
Switch(config-if)#int e0/2
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 20
Switch(config-if)#int e0/3
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 20
Switch(config-if)#do sh vlan brief
```
