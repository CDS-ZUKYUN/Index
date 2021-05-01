# 1-5 Proxy運作(4/24-day26)

* * *

## Proxy Server

參照:squid_proxy.pptx 

代理通訊協定http，也可以代理ftp、ping不代理、ntp通訊協定(對時)

代理伺服器（Proxy），是一種重要的電腦資安功能，也是特殊的網路服務，允許用戶端透過它與另一個網路服務進行非直接的連線，也稱「網路代理」。代理伺服器有利於保障網路安全，防止攻擊。

代理伺服器（proxy server）設置的兩個主要目的：加強網路安全及提升網路使用效率(cache)。 


- 兩個權威網站
serverfault
stackoverflow

### 1. 安裝Squid for proxy

```
~$ sudo apk update
~$ sudo apk add squid
#啟動squid (停止、重啟)
~$ sudo rc-service squid start (stop) (restart)
#查看squid運行狀態
~$ sudo rc-service squid status 
#讓squid開機自動執行 (del)
~$ sudo rc-update add squid  (del)
```
![](https://i.imgur.com/EOO5gpf.png)

### 2. proxy squid設定檔案 /etc/squid/squid.conf

#備分
~$ sudo cp /etc/squid/squid.conf /etc/squid/squid.conf.bk



- Acl設定方式 存取管理清單 




Acl 宣告 ip
acldomain 宣告 domain name
.domain name
Teacher這個規則 
Src  ip位置落在192.168.1.0/24 
acl lunch time MTWHF 12:00-15:00 
什麼時候開門營業


**1.實作acl設定規則**

![](https://i.imgur.com/jadGcTX.png)

![](https://i.imgur.com/3Vx0f3w.png)

![](https://i.imgur.com/knJANvQ.png)
error

![](https://i.imgur.com/Kmv85QP.png)

![](https://i.imgur.com/oGYhEfc.png)

![](https://i.imgur.com/kTky4ZC.png)


解說:

![](https://i.imgur.com/be25W6y.png)

ok

1.AR23301 filter 把window擋掉
2.window firefox 設proxy http:AP23301 port 3128
結論 win 無法ping 但可以瀏覽網站
