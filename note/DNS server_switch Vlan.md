# DNS server設定兩種網路透過switch Vlan分配IP給兩台電腦 
![image](https://user-images.githubusercontent.com/62127656/148355162-b96db56e-3368-4f42-9600-9c38ec1be1ac.png)

switch set vlan
```
Switch(config)#vlan 10
Switch(config-vlan)#exit
Switch(config)#vlan 20
Switch(config-vlan)#exit
Switch(config)#int e0/0
Switch(config-if)#switchport trunk encapsulation dot1q
Switch(config-if)#switchport mode trunk
Switch(config-if)#int e0/1
Switch(config-if)#switchport access vlan 10
Switch(config-if)#switchport mode access
Switch(config-if)#int e0/2
Switch(config-if)#switchport access vlan 20
Switch(config-if)#switchport mode access
```
router 
```
int e0/0.10
encapsulation dot1Q 10
ip addr 192.168.10.254 255.255.255.0
no shut
ip dhcp pool mypool1
network 192.168.10.0 255.255.255.0
default-router 192.168.10.254 
dns-server 8.8.8.8
ip dhcp excluded-address 192.168.10.250 192.168.10.254

int e0/0.20
encapsulation dot1Q 20
ip addr 192.168.20.254 255.255.255.0
no shut
ip dhcp pool mypool2
network 192.168.20.0 255.255.255.0
default-router 192.168.20.254 
dns-server 8.8.8.8
ip dhcp excluded-address 192.168.20.250 192.168.20.254
```
pc
```
ip dhcp
```
![image](https://user-images.githubusercontent.com/62127656/148355270-d621f59b-6c37-47a9-b4b7-2886ffc1e2bd.png)
