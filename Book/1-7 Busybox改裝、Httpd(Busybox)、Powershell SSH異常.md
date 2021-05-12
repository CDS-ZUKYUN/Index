# 01-7 Busybox改裝、Httpd(Busybox)、Powershell SSH異常 

>date_tag: 0511
>
>pptx_tag: SRE專題研究_高可靠性企業應用系統實作.pptx

## 1. busybox改裝(增加httpd功能)

**container示例(前置):**

>1. ssh alp_ctn
> 
>2. 啟動container(t1) 用終端機跑sh 
> 
>3. 下載 Busybox 執行檔
>
> 
> 
> check: busybox | grep httpd
 
```
1. ssh bigred@<CTN.ALP.Docker IP>

2. docker run --name t1 -it alpine sh
/ # busybox | grep httpd
/ # which busybox

3. 
/ #  wget 'https://busybox.net/downloads/binaries/1.31.0-defconfig-multiarch-musl/busybox-x86_64' -O busybox1.31
安裝 Busybox 執行檔
/ #  ls
/ #  chmod +x busybox1.31
/ #  which busybox
/ #  mv busybox1.31 bin/busybox
檢查busybox改裝
/ # busybox(1.31) | grep httpd
```
 
 
## 2. Busybox Httpd 網站伺服器


>1. 製作網站目錄及首頁
>
>2. 啟動 Busybox Httpd 網站伺服器
>
>3. 安裝網頁工具(curl、elinks)
>
>4. 測試httpd


```
1.
/ # mkdir www
/ # echo '<h1>Busybox HTTPd</h1>' > www/index.html

2.
/ # busybox httpd -p 8080 -h www

3.
/ # apk update
/ # apk add elinks curl

4.
取得網頁
/ # curl http://localhost:8080
<h1>Busybox HTTPd show out!!!</h1>

檢視網頁 (elinks是瀏覽器，前端結果顯示)
/ # elinks -dump 1 http://localhost:8080

/ # exit

```


## 3. SSH連線出現錯誤 
 
>做法:公鑰不合，刪掉公鑰再重連

ssh錯誤資訊:

![](https://i.imgur.com/hyMKj9l.png)
 

```
ssh-keygen -R 192.168.2.151

ssh bigred@192.168.2.151
```


<br /><br />
###### tags: `Alpine`









