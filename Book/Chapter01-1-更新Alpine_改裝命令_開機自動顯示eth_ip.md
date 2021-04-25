# Alp_Chapter 01-1.Alpine系統更新、改裝命令、自動化autolization(show eth ip)

* * *

<h2 id=""></h2>

1.系統apk更新，能寫在文字檔
```
sudo apk update
sudo apk upgrade
apk add nano tree bash net-tools iptables wget curl grep procps unzip zip sudo
```
</br>

2.系統用途規劃
</br>

3.alias改裝命令(/etc/profile)


```
# alias block

alias ping='ping -c 4'
alias dir='ls -al'
alias ps='ps -eo user,pid,cmd,%cpu,%mem'
```
</br>

3.自動化autolization(/etc/profile)
- 顯示網卡ip

```
# autolization block(1 show ip)

gw=$(route -n | grep -e "^0.0.0.0 ")
export GWIF=${gw##* }
ips=$(ifconfig $GWIF | grep 'inet ')
export IP=$(echo $ips | cut -d' ' -f2 | cut -d':' -f2)
export NETID=$(route -n |grep " U " | grep $GWIF |tr -s ' ' |cut -d ' ' -f1)
export GW=$(route -n | grep -e '^0.0.0.0' | tr -s \ - | cut -d ' ' -f2)
export PATH=/home/bigred/bin:$PATH
clear
echo "Welcome to Container Trainer V 21.02 (Alpine Linux : `cat /etc/alpine-release`)"
d=$(ls /sys/class/net)
#mount=$(ifconfig | grep eth | wc -l)

for x in $d
do
if [ "$x" != "lo" ]
then
  ip=$(ifconfig $x | grep 'inet ' | tr -s ' ' | cut -d' ' -f3 | cut -d ':' -f2 )
  echo "$x: " $ip
fi
done

```

<br /><br />
###### tags: `Alpine`