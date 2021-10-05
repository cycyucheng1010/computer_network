# 20211005
## TFTP
* 簡單檔案傳輸協定也稱小型檔案傳輸協定（Trivial File Transfer Protocol, TFTP）。
* 透過少量記憶體就能輕鬆實現
```
virtual machine:

sudo yum install -y xinted tftp-server
sudo vim /etc/xinetd.d/tftp
:
server_args = -c -s /var/lib/tftpboot
diable      = no
:
sudo chmod 777 /var/lib/tftpboot
```
## OpenWrt
* OpenWrt是適合於嵌入式裝置的一個Linux發行版。
* 不是一個單一、靜態的韌體，而是提供了一個可添加軟體套件的可寫的檔案系統。

## 參考資料
* [[CentOS 7] 檔案傳輸界的隱形冠軍 - TFTP 伺服器](http://blog.itist.tw/2016/09/install-a-tftp-server-on-centos-7.html)
## 實驗一
* 可直接對序列阜，因為serial一對一
