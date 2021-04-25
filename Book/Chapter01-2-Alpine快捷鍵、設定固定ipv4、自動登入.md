# Alp_Chapter 01-2.Alpine快捷鍵、設定固定ipv4、自動登入

* * *

<h2 id=""></h2>

提醒:要記得改主機名稱(/etc/hostname)

0.快捷功能 cut&paste,code-row-nomber
```
ctrl+k & ctrl +u
shift +alt +3
```
</br>


1.設定固定ipv4(/etc/network/interface)
空模板/範例(雙網卡):
```
sudo nano /etc/network/interface

-------------------------------------
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
        address 
        netmask 
        gateway 
        hostname alptest

auto eth1
iface eth1 inet static
        address 
        netmask 
--------------------------------------
auto eth0
iface eth0 inet static
        address 172.30.0.1
        netmask 255.255.224.0
        gateway 172.30.31.254
        hostname alptest

auto eth1
iface eth1 inet static
        address 172.30.63.254
        netmask 255.255.224.0
```
</br>

2.Alpine自動登入

- 1.為了run agetty套件，安裝util-linux (不知道agetty為何)
```
sudo apk add util-linux
```

- 2.改命令tty1::(/etc/inittab)
```
sudo nano /etc/inittab
tty1::respawn:/sbin/agetty --autologin bigred --noclear 38400 tty1
```

範例結果:

- 1.

![](https://i.imgur.com/EYklGff.png)


- 2.

ttys0不用改
![](https://i.imgur.com/Cw4tUmM.png)



<br /><br />
###### tags: `Alpine`