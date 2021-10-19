# 2021.10.19 
## port forwarding
* 當有從外部進來的需求被送到路由器時，這個需求會依據他的通訊協定（例如網頁 http），或是使用者指定的 Port 號碼，由路由器將這個需求依照 Port 號碼送到指定的裝置去。
![image](https://user-images.githubusercontent.com/62127656/137851100-e199c9ff-4d57-4c73-a706-6f95c8eb8cd7.png)
## RIP
* 路由資訊協定（英語：Routing Information Protocol，縮寫：RIP）是一種內部網路關協定（IGP），為最早出現的距離向量路由協定。
* 路徑表更新:
  1. 30s 更新一次
  2. 超過 180s 停止運作
  3. 超過 240s 刪除路由
![image](https://user-images.githubusercontent.com/62127656/137854586-590eb5fa-f92b-4ebb-aaa0-0ab4e63bbcd9.png)
![image](https://user-images.githubusercontent.com/62127656/137855277-53f7a3ac-5d6c-44c6-bc45-454f400ceb6f.png)
### 實驗一

![image](https://user-images.githubusercontent.com/62127656/137869237-19baa89c-f660-4179-8bee-3b7b952707d7.png)


* r1
```
Router>en
Router#conf t
Router(config)#hostname r1
r1(config)#int e0/0
r1(config-if)#ip addr 12.1.1.1 255.255.255.0
r1(config-if)#no shut
r1(config-if)#exit
r1(config)#router rip
r1(config-router)#network 12.0.0.0
r1(config-router)#do show ip int brief
r1(config)#do show ip route
r1(config)#exit
----等r2 r3設置完成 ----
r1#ping 23.1.1.3

```
* r2
```
Router>en
Router#conf t
Router(config)#hostname r2
r2(config)#int e0/0
r2(config-if)#ip addr 12.1.1.2 255.255.255.0
r2(config-if)#no shut
r2(config-if)#int
r2(config-if)#int e0/1
r2(config-if)#ip addr 23.1.1.2 255.255.255.0
r2(config-if)#no shut
r2(config-if)#exit
r2(config)#router rip
r2(config-router)#network 12.0.0.0
r2(config-router)#network 23.0.0.0
r2(config-router)#do show ip int brief
```
* r3
```
Router>en
Router#conf t
Router(config)#hostname r3
r3(config)#int e0/0
r3(config-if)#ip addr 23.1.1.3 255.255.255.0
r3(config-if)#no shut
r3(config-if)#exit
r3(config)#router rip
r3(config-router)#network 23.0.0.0
r3(config)#do show ip route
```

![image](https://user-images.githubusercontent.com/62127656/137866211-9ee1ff2b-f9aa-4555-b7bd-6cfccc07523c.png)

* 清除
```
no router rip 
```
## EIGRP
## 參考資料
* [RIP v1與RIP v2路由協議對比分析](https://blog.xuite.net/lichangying/wretch/176501055-RIP+v1%E8%88%87RIP+v2%E8%B7%AF%E7%94%B1%E5%8D%94%E8%AD%B0%E5%B0%8D%E6%AF%94%E5%88%86%E6%9E%90)
* [深入了解IP位址與子網路遮罩](https://www.netadmin.com.tw/netadmin/zh-tw/technology/D5162EE38674405EADB022E0802A05B2)
* [通訊埠轉發 Port Forwarding 設定教學：如何從外面連回家中 NAS？](https://ningselect.com/30752/58/)
