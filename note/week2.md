# week2
* ``` > ``` : user model
* enable切換到privilege mode
* ``` # ``` : prvilege mode
* 利用exit離開privilege mode
* ```config```: configuration mode
* ```conf t```:configure terminal
* 第一個封包失敗，因為做arp解析。 ```show arp ```
* write memory ```wrm```
## CISCO 設備
* NVRAM :start up cinfiguration file
* RAM : runing configuration
* Flash : OS
## 實驗一
### 設定router
```
en
conf t
int e0/1
ip addr 192.168.1.254 255.255.255.0
no shut 
int e0/2
ip addr 192.168.2.254 255.255.255.0
no shut 
do show ip int brief
```
### 電腦1
```
192.168.1.1 255.255.255.0 192.168.1.254

```
### 個別電腦
```
192.168.2.1 255.255.255.0 192.168.2.254

```
ip dhcp pool 名字
