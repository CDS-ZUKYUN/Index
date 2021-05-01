# 01-4.Alpine建置DHCP server

* * *

<h2 id=""></h2>

提醒1:切網段前10後5


## 1.Alp建置DHCP server

- 安裝DHCP server apk
```
$ sudo apk update
$ sudo apk add dhcp
(1/4) Installing libgcc (10.2.1_pre1-r3)
(2/4) Installing dhcp (4.4.2-r3)
Executing dhcp-4.4.2-r3.pre-install
(3/4) Installing dhcp-server-vanilla (4.4.2-r3)
(4/4) Installing dhcp-openrc (4.4.2-r3)
Executing busybox-1.32.1-r5.trigger
OK: 925 MiB in 172 packages
```

### error1 私有ip無法上網

![DHCP3](https://i.imgur.com/y34V40k.png)

- 解決方法

  P1第一，開啟forwarding;第二，增加偽裝規則
  
```
sudo nano /etc/local.d/route_set.start

#!/bin/bash
route add -net [] netmask [] gw []
sudo iptables -t nat -A POSTROUTING -o eth0 ! -d ip_wholenet/mask -j MASQUERADE
```

![DHCP5](https://i.imgur.com/GUlsTs0.png)

/etc/sysctl.conf
```
net.ipv4.ip_forward=1
# content of this file will override /etc/sysctl.d/*
```


/etc/local.d/route_set.start
```
sudo iptables -t nat -A POSTROUTING -o eth0 ! -d 172.30.0.0/255.255.0.0 -j MASQUERADE
```

問題解決

![DHCP6](https://i.imgur.com/q1kjAjm.png)



## 編寫DHCP server設定檔(r1)

r1 --> winxp king
$ sudo nano /etc/dhcp/dhcpd.conf
網段172.30.47前半 48後半開始
```
subnet 172.30.32.0 netmask 255.255.224.0 {
  option domain-name "right.io";
  option domain-name-servers 172.30.63.254, 8.8.8.8;
  option routers 172.30.63.254;
  range 172.30.48.0 172.30.63.249;
}
```
sudo rc-update add dhcpd
sudo rc-service dhcpd start

![DHCP8](https://i.imgur.com/54pdCn8.png)

-------------------------------




<br /><br />
###### tags: `Alpine`
