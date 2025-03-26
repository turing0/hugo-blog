+++
title = 'Nginx 反向代理 API'
slug = 'Nginx Reverse Proxy Api'
date = '2025-03-26T13:40:10+08:00'
draft = false
categories = [""]
tags = [""]

+++

有的 API 服务会限制某些国家访问，我们就可以搭建一个反代 API 的服务绕过此限制，用不限制的服务器的 IP 作为转发。

比如 https://api.binance.com 限制美国 IP 访问，本文以这个为例来进行搭建反代 Binance API 的服务。



## 安装 Nginx 

准备一个能正常访问 Binance API 的服务器，安装 Nginx。

```bash
sudo apt update && sudo apt install -y nginx
```





## 配置反代 API 服务

编辑 Nginx 配置文件：

`vi /etc/nginx/sites-available/default`



添加内容：

```
server {
    listen 80;
    server_name proxybinance.xxx.com;  # 你的域名

    location / {
        proxy_pass https://api.binance.com/;  # 代理到目标 API
        proxy_set_header Host $proxy_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

```

`proxybinance.xxx.com` 换为你自己的域名，记得 DNS 解析到服务器。





重启 Nginx 服务：

```bash
sudo systemctl reload nginx
```



## 测试反向代理

将需要用到 Binance API 的地方的域名换为 `http://proxybinance.xxx.com` 即可。

如果需要 https，则用 [certbot 申请证书](https://blog.laphel.com/posts/nginx-reverse-proxy-service/#%E7%94%B3%E8%AF%B7-ssl-%E8%AF%81%E4%B9%A6) 就好。





























