# 1. Install Alpine

>參照1-0系列pptx食用

* * *

<h2 id="iso">step1.下載Alpine_ISO映像檔</h2>


Alpine 官網 : https://alpinelinux.org/downloads/。

![Alp_ISO_file](https://i.imgur.com/UYZGJ3w.png)


---
<h2 id="VMconfig">step2.VMware_Alp_config</h2>

1. 自己安裝OS

![os_install_byself](https://i.imgur.com/q1kvlzG.png)
<br />
<br />

2. 注意創建(Create)選的版本:

alpine-standard-3.13.4-x86_64.iso (註:此ISO是5.x kernerl)1<br />
![VMw_config_p1](https://i.imgur.com/XFHRtcA.png)<br />
<br />


3. 名稱、路徑命名需有意義(不倚靠感覺):

例如:做webserver用，那就最好如下例做命名；並且，請注意將OS放在跑最快的C槽，設定的路徑要簡單好找。<br />
![VMw_config_p2](https://i.imgur.com/1FyrkAH.png)<br />
<br />

4. 使用空間必須根據狀況的評估去設(不可靠感覺):

` 例如:一間公司做file server使用，估300GB就夠，但考慮未來性及工程師管理方面，我們就必須多留空間。
請從600GB開始，給自己跟別人空間，現在都沒有再用FAT32(4G上限)，所以請用單檔存`

![VMw_config_p3](https://i.imgur.com/lwOZArj.png)
<br />




5. 記憶體多大:

一般商業用Web Server 2GB夠用(1個人對server進行web connect約佔1K的ram)
記憶體能負擔，之後可能的問題便是頻寬的挑戰。

Youtube 會動會跳的不行Ram跟HD都要新境界的大空間才行。

6. 核心多少:

因為只需要建立布告欄功能型的網站，因此處理的core兩個就夠了

* 豆知識Printer: 

產生檔案，丟給網路印表機影印


![set_ram](https://i.imgur.com/FZVI0r7.png)
<br />


Tip 

將網路Bridge推出，以公有ipv4連外網安裝，之後比較不會有無法更新之類的問題。<br />
![VMw_config_p3](https://i.imgur.com/J0xk1Ci.png)<br />
<br />



---
<h2 id="alp_os_config">step3.Set_Alpine_OS_Config</h2>

* 介面網卡-ipv4手動設定(win10):

若不是以NAT而是Bridge mode去安裝，需調回學校的手動配置ip，安裝的時候才讀的到mirror source net。(課堂練習有改成DHCP過，要注意)

![mirror number(1-0j)_error](https://i.imgur.com/2YRPfEY.png)
<br />
<br />

### 正式設定Alp安裝配置

1. 初始安裝畫面:

請輸入root登入

![start_screen](https://i.imgur.com/qO5z7Ig.png)

補充知識:

起初Alpine並無具有sudo權限的帳戶(沒有要我們設)；反之，Ubuntu則有。通過設定
Yourname bigred(給予帳號sudo權)，username bigred(創帳號)
上面兩者相同，將會有merge的效果。成為具有sudo權的帳號bigred。
<br />
<br />

2.  Alpine預設命令(安裝系統)

輸入： setup-alpine 

![initial_cmd](https://i.imgur.com/JMBpUwK.png)

[注意]
安裝過程使用問答方式，若回答想要反悔，只能透過 Ctrl + C 重來(此段引用彥榮老師的ppt)。
<br />
<br />

3.  Alpine鍵盤配置

設定台式鍵盤配置

`Select keyboard layout:tw `

設定備用鍵盤配置

`Select variants ... :tw
`

![keyboard_layout](https://i.imgur.com/mYe11OT.png)
<br />
<br />

4.  使用者名稱、網卡、DHCP配置

輸入localhost name

`[localhost] alpine`

eth0 網卡名稱 (alpine)，選eth0網卡來設置(Enter)

`[eth0]`

DHCP留空就用自動模式(如下圖)，DHCP(server)自動抓ip，非手動
(n)不自己設

`[dhcp] [手動直接加ip在後]
enter [subnet mask] enter [gw ip]`


![user_alpconfig1](https://i.imgur.com/OKBuI47.png)
<br />
<br />

5.  設定密碼

New password:root

![set_passwd](https://i.imgur.com/B67BgnV.png)
<br />
<br />

6.  設定時區、Proxy、NTP(時間伺服器)

時區:亞洲 台北

NTP(時間伺服器):
預設之自動校時同步伺服器

Proxy:內網聯外網公司不允許，所以通過proxy server(設ip)，none沒有設proxy


`微軟的active directory 系統，管理所有人的帳號，密碼 (差15分鐘時間就無法連線)`

`時間不一IOT感測網路資料會有問題會無法使用`

![set_time_prox_NTP](https://i.imgur.com/SxyH6J0.png)
<br />
<br />

7.  設定Alp update source net

有1-60的網站能作系統的更新(37示範過有點保障)

選國家高速網路中心(代號?)

俄羅斯代號6

![set_apl_update_net](https://i.imgur.com/oYhrJHb.png)
<br />
<br />

8.  安裝裝遠端連線管理Open ssh

![install_opssh](https://i.imgur.com/CRcaeyN.png)
<br />
<br />

9.  選硬碟安裝(只有sda這顆)
  
![select_hd](https://i.imgur.com/GFAi7nM.png)
<br />
<br />

10.  用sda硬碟裝sys(系統)

![sda_install_aplsys](https://i.imgur.com/jQbgOrO.png)
<br />
<br />

11.  格式化硬碟裝(y)
  
![wait_done](https://i.imgur.com/Finp6il.png)
<br />
<br />

12.  安裝完成

![finish](https://i.imgur.com/9VFqqbE.png)

安裝至硬碟後須重新開機，並退出 iso .
輸入： reboot(此段引用彥榮老師的ppt)。

<br /><br />
