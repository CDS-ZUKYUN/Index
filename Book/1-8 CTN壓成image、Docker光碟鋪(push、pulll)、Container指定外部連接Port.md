# 01-8 CTN壓成image、Docker光碟鋪(push、pulll)、Container指定外部連接Port

>date_tag: 0511
>
>pptx_tag: SRE專題研究_高可靠性企業應用系統實作.pptx



## 1. Container壓成image
---


>1. 開啟t1 container
>
>2. 指令commit把t1 container包成image
>
>3. 登入zukyun docker hub，push image



```
1. $ docker run --name t1 -it alpine sh

2. 
$ docker ps -a
$ docker commit t1 zukyun/t1
註:           CTNname     image name
```

## 2. docker光碟鋪(push/pull)
---
>1. 推(push)image
>
>2. docker關container
>
>3. 使用自製 zukyun/t1 image (含httpd推網頁)
>
>4. 測試test1 container
```
1.
$ docker login 
$ docker push zukyun/t1
$ docker logout

2.
docker rm t1 或者 docker rm XXXX(container id)
註: docker rm -f t1 (強制刪container)

3.
docker run --name test1 -d zukyun/t1 busybox httpd -f -p 8080 -h www
註: 這是對的，-f foreground 至關重要


docker run --name test1 -d zukyun/t1 busybox httpd -p 8080 -h www 

docker ps -a
註: 這是錯的,container背景run，因 httpd 沒在前景啟動, 以致 test1 貨櫃主機沒啟動，STATUS:Exited

4.
看test1 container ip
$ docker exec test1 hostname -i
172.17.0.2

砍test1 container httpd推的網站
$ curl http://172.17.0.2:8080
<h1>Busybox HTTPd</h1>


格式: none
Example: none

Tip: none
```

## 3. Container指定外部連接Port
---
>1. 檢查當前啟動那些container
>
>2. 重新建立test1 CTN, 並指定外部連接 Port
>
>3. 砍container網頁來測試

```
1. docker rm -f test1
註: 以強制方式移除 test1
 
2. docker run --name test1 -d -p 80:8080 zukyun/t1 busybox httpd -f -p 8080 -h www 

3. curl http://localhost:80

win10測試:
查 ALP ip, 用win broswertest

```


<br /><br />
###### tags: `Alpine`














