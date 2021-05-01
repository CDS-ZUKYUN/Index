# Alp_Chapter 02. Iptable運作(4/24-day26)


* * *



參照食用:0424_iptables.pptx (26Day).pptx

- iptables 
就是Linux 作業系統的防火牆，存在「表（tables）」、「鏈（chain）」和「規則（rules）」三個層面。

![7](https://i.imgur.com/D0nmejC.png)

![](https://i.imgur.com/EI7JRht.png)



- user space 
>>使用者使用的系統空間，低權限，不可設ip iptable(ip table指令)，除非...



- alp查詢module

`lsmod | grep iptable`  


- filter table
>>過濾封包


- 封包
>>從網卡接收近來，路由routing table判斷 電腦依據路由表，看從哪個gw送封包



## Alp-iptables實作

1.套件安裝
2.版本
3.查看filter rule iptable

```
1 $ sudo apk add iptables

2 $ sudo iptables –V
iptables v1.8.6 (legacy)

3 $ sudo iptables -L -n
Chain INPUT (policy ACCEPT)
target     prot opt source               destination

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
# -t table名 可以指定table default是filter
```


4.增加規則進filter-INPUT
`sudo iptables -I INPUT -s 10.233.0.129 -j DROP
-s source`

![](https://i.imgur.com/uhAKXt5.png)


5.刪除規則filter-INPUT
`sudo iptables -D INPUT -s 10.233.0.129 -j DROP
-s source`

![](https://i.imgur.com/Xm5PUZw.png)


6.偽裝，增加規則進nat-POSTROUTING

![6](https://i.imgur.com/gAjMcmn.png)


# **7.尚未完全理解**
![](https://i.imgur.com/V4fC8CD.png)



## routing rule table working(nat、filter)


**兩種routing rule table(filter(default),nat)**
下指令不指定table，會指向filter table。
- A條件判斷
路由判斷(看路由表) 若封包的source ip是我這台電腦的(例如:AR)，那麼我就往上走，經過一連串規則的判斷，最後到的nat_POSTROUTING，然後output出封包。

- B條件判斷
路由判斷 若封包的source ip不是自己，看routing table，看要怎麼傳，有開forwarding的情況下，最後到的nat_POSTROUTING，然後output出封包;沒有開forwarding，就不回傳封包(不知道怎麼回給source)




![16](https://i.imgur.com/KLdLYKQ.png)



### iptable 實作 (有port就有ip)

![70145](https://i.imgur.com/GzlEdAQ.jpg)



AR23303 阻擋 AR23304 
(增加規則進filter table)

`sudo iptables -I INPUT -s 10.233.0.192/26 -j DROP` 

![1](https://i.imgur.com/Z1X2rTS.png)

![2](https://i.imgur.com/1FfytCt.png)

![3](https://i.imgur.com/5K4F8kC.png)


AR23303阻檔queen網段

![4](https://i.imgur.com/3nKboED.png)

![5](https://i.imgur.com/5z2ukft.png)

![6](https://i.imgur.com/tpQ4glw.png)


- 查看路由表(預設filter table)
sudo iptables -L -n

![7](https://i.imgur.com/fbameTO.png)


- 查看路由表(-t 指定nat table)

![](https://i.imgur.com/LOKavBC.png)

- 清空filter/nat table 規則

![](https://i.imgur.com/EiAkTrg.png)


- 刪除規則(預設filter table)

![15](https://i.imgur.com/WaqOE6q.png)


iptable(.241/.189-AR)運作概念圖

![14](https://i.imgur.com/N9hXXi8.png)


### 噴error

- 錯誤

![](https://i.imgur.com/9Kml2FL.png)

第一行，封包一定要到nat-POSTROUTING才能-o output
第二行，封包一定要到nat-POSTROUTING才能-j jump(有爭議待釐清，尚未)



## tag 尚未理解
$ sudo iptables -A FORWARD -p tcp --dport 80:443 -j DROP

$ sudo iptables -A FORWARD -s 10.233.0.0/24 -p tcp --dport 80:443 -j DROP


</br >
