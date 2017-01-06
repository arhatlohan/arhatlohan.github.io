---
title: shadowsocks server 配置
date: 2016-12-28 20:57:36
tags: [VPN, Shadowsocks]
---

### Install
#### Debian/Ubuntu
```
apt-get install python-pip
pip install shadowsocks
```

#### CentOS
```
yum install python-setuptools $$easy_install pip
pip install shadowsocks
```

---

### Usage
```
ssserver -p 443 -k password -m rc4-md5
```
如果要后台运行：
```
sudo ssserver -p -k password -m rc4-md5 --user nobody -d start
```
如果要停止：
```
sudo ssserver -d stop
```

日志文件：
```
sudo less /var/log/shadowsocks.log
```

或者,使用配置文件：
配置文件：`/etc/shadowsocks.json`
```
{
    "server":"172.31.17.22", //对于没有独立ip使用NAT上网的模式的，要查看自己ip
     "server_port":878, //自定义
     "local_port":108,
     "password":"×××××××",
     "timeout":600,
     "method":"aes-256-cfb"
}

```
命令：
```
ssserver -c /etc/shadowsocks.json -d start

```






