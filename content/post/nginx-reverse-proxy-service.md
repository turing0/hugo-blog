+++
title = 'Nginx 反代服务'
slug = 'Nginx Reverse Proxy Service'
date = '2025-03-12T16:56:10+08:00'
categories = [""]
tags = ["nginx"]

+++



比如有个 fastapi 服务在 8001 端口，现在想要实现通过域名访问，怎么做呢？

这就需要 Nginx 反代了。

以下我使用 Ubuntu 服务器进行操作。



## Nginx 反代配置

首先需要将域名解析到服务器的 IP 地址，然后继续。



编辑 Nginx 配置文件：

`vi /etc/nginx/sites-available/default`

设置反向代理，将请求转发到 FastAPI 服务的 8001 端口：

```nginx
server {
    listen 80;
    server_name example.com;  # 域名

    location / {
        proxy_pass http://127.0.0.1:8001;  # 服务地址
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

 `proxy_pass` 指向了 FastAPI 服务所在的地址 `127.0.0.1:8001`，只要访问这个域名的所有请求都会被转发到 FastAPI 服务。



检查 Nginx 配置：`sudo nginx -t`

如果配置正确。就会看到输出：

```bash
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```



配置没问题，重新加载 Nginx 让他生效：

```bash
sudo systemctl reload nginx
```



现在，通过上面的域名访问，就可以啦！

下一步，添加 ssl。



## 添加 SSL

这里我们用 Let's Encrypt 免费的 SSL 证书来实现 HTTPS 加密。



### 安装 Certbot

Certbot 是一个由 Let's Encrypt 提供的自动化工具。

安装 Certbot：

```bash
sudo apt update
sudo apt install certbot python3-certbot-nginx
```



### 申请 SSL 证书

使用 Certbot 直接为 Nginx 配置 SSL 证书：

```bash
sudo certbot --nginx -d example.com
```

这个命令会让 Certbot 自动与 Let's Encrypt 交互，申请证书，并自动配置 Nginx 来支持 HTTPS。

- `--nginx` 选项表示 Certbot 会自动修改你的 Nginx 配置以启用 SSL。
- `-d example.com` 是刚才配置的域名。



如果有多个域名或子域名，也可以这样指定：

```bash
sudo certbot --nginx -d example.com -d www.example.com
```



来看看 certbot 添加了什么，执行：

```bash
cat /etc/nginx/sites-available/default
```

可以看到：

```
server {
    server_name example.com;

    location / {
        proxy_pass http://127.0.0.1:8001;  # FastAPI 服务地址
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}

server {
    if ($host = img.example.com) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


    listen 80;
    server_name img.example.com;
    return 404; # managed by Certbot


}
```

certbot 为我们添加了 443 的监听以及 https 跳转。





### 确认自动配置

Certbot 会在成功申请证书后，自动为 Nginx 配置 SSL。可以通过以下命令检查 Nginx 配置文件是否正确：

```bash
sudo nginx -t
```

没有错误，老样子，重新加载 Nginx 配置：

```bash
sudo systemctl reload nginx
```

到这里就可以用我们的域名通过 https 访问啦！



### 自动续期

Let's Encrypt 的证书有效期是 90 天，因此需要定期续期。可以使用 Certbot 自动续期，运行以下命令测试续期功能：

```bash
sudo certbot renew --dry-run
```

如果一切正常，你可以设置一个定时任务（cron job）来自动续期证书。

打开 cron 编辑器：

```bash
sudo crontab -e
```

添加以下行，每天检查并自动续期证书：

```bash
0 3 * * * certbot renew --quiet && systemctl reload nginx
```

这个任务会每天凌晨 3 点检查证书是否需要续期，并在成功续期后重新加载 Nginx。



Easy ~

