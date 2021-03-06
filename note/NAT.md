# 靜態NAT
![image](https://user-images.githubusercontent.com/62127656/148354896-31b2a296-e7cd-4854-8a4b-cc9c9e8563fe.png)
R4 (Server)
```
R4(config)#int e0/0
R4(config-if)#ip addr 24.1.1.4 255.255.255.0
R4(config-if)#no shut
R4(config-if)#exit
R4(config)#ip route 0.0.0.0 0.0.0.0 24.1.1.2
R4(config)#line vty 0 4
R4(config-line)#password 123
R4(config-line)#login
R4(config-line)#transport input telnet
```
R2 邊緣路由器
```
R2(config)#int e0/0
R2(config-if)#ip addr 12.1.1.2 255.255.255.0
R2(config-if)#no shut
R2(config-if)#int e0/1
R2(config-if)#ip addr 23.1.1.2 255.255.255.0
R2(config-if)#no shut
R2(config-if)#int e0/2
R2(config-if)#ip addr 24.1.1.2 255.255.255.0
R2(config-if)#no shut
R2(config-if)#exit
R2(config)#do telnet 24.1.1.4
Trying 24.1.1.4 ... Open
User Access Verification
Password:
R4>
```
R3 外網路由器
```
R3(config)#int e0/0
R3(config-if)#ip addr 23.1.1.3 255.255.255.0
R3(config-if)#no shut
```
R2
```
R2(config)#int e0/2
R2(config-if)#ip nat inside
R2(config-if)#int e0/1
R2(config-if)#ip nat outside
R2(config-if)#exit
R2(config)#ip nat inside source static tcp 24.1.1.4 23 23.1.1.2 23
R2(config)#do sh ip nat translations
Pro Inside global      Inside local       Outside local      Outside global
tcp 23.1.1.2:23        24.1.1.4:23        ---                ---
```
R3
```
R3#telnet 23.1.1.2
Trying 23.1.1.2 ... Open
User Access Verification
Password:
R4>
```
