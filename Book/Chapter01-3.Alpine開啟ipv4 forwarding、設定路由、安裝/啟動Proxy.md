# Alp_Chapter 01-3.Alpine開啟ipv4 forwarding、設定路由、安裝/啟動Proxy

* * *

<h2 id=""></h2>

提醒1:ssh連線能層層去連線
提醒2:ping有去有回，對方要新增route，才能回應。

1.Alp開啟ipv4 forwarding

- 永久開啟(sudo nano /etc/sysctl.conf)
```
net.ipv4.ip_forward=1
# content of this file will override /etc/sysctl.d/*
```

- 暫時開啟(sudo nano /proc/sys/net/ipv4/ip_forward)
```
1
```

-------------------------------

2.開機設定路由(sudo nano /etc/local.d/route_set.start)

- 0 增加路由進路由表

情境紀錄:
當king ping p1(alpProxy)能透過r1 forwarding，顯示 timeout error
表示，king知道p1在哪，但是p1不曉得，因此加下面網路路由172.30.32.0

```
#!/bin/bash
route add -net 172.30.32.0 netmask 255.255.224.0 gw 172.30.0.1
```

- 1 給執行權限
- 2 啟用開機執行檔功能(add local)
- 3 重新開機
- 4 檢查路由表
```
1 sudo chmod +x /etc/local.d/route_set.start
2 sudo rc-update add local
3 sudo reboot
4 route -n
```

-------------------------------

3.安裝/啟動Proxy (不需要開啟forwarding)

- 1. 安裝Squid for proxy(alp-Proxy_p1)

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




範例結果:

情境:window ping的到p1，但是無法用browser瀏覽網頁。
因此p1要開啟proxy
![proxy1](https://i.imgur.com/nUsqbD9.png)

- 2. winxp(king) browser test

**設定proxy(D:p1_ip)**

![proxy2.png](https://i.imgur.com/kncLr1e.png)

**king chrome成功上網(透過p1)**

![proxy3.png](https://i.imgur.com/n7gH1k6.png)



<br /><br />
###### tags: `Alpine`