# 2021.09.28
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
int e0/0
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
## 實驗二
### 設定dhcp in router
```
ip dhcp pool mypool
netwrok 192.168.1.0 255.255.255.0
default-router 192.168.1.254 
dns-server 8.8.8.8
dns-server exclude 192.168.1.250 192.168.1.254 (排除一些不想分配出去的ip)

ip dhcp pool mypoo2
netwrok 192.168.2.0 255.255.255.0
default-router 192.168.2.254
dns-server 8.8.8.8
dns-server exclude 192.168.2.250 192.168.2.254
```
```
 PC : ip dhcp

```
## 實驗三
1. 設定本機帳號
```
(config)#username cisco password ccna   建立帳號cisco密碼nnca(密碼未加密)
(config)#username cisco secret ccna         建立帳號cisco1密碼nnca(密碼加密)
同一帳號僅可選一種方式設定密碼
若要取消password可使用
(config)#username cisco nopassword
取消secret使用
(config)#username cisco nosecret
```
2. 設定加密方式(產生加密key)
```
(config)#ip domain-name ccna.com          設定domain-name為ccna
(config)# host name h1
(config)#crypto key generate rsa               產生rsa金鑰
How many bit in the modulus[512]:1024  使用1024bit加密(預設512)
```
3. 啟用SSH/Telnet連線
``` 
(config)#ip ssh version 2                         使用ssh v2協定
(config)#line vty 0 4                                開啟0~4vty連線(即最大連線人數5人)
(config-line)#login local                          啟用密碼(login)及帳號(local) 
(config-line)#transport input ssh            啟用ssh
```
