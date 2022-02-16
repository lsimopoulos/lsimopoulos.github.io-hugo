+++
date = "2022-02-16T9:00:00+02:00"
archives = ["2022/02"]
tags = ["Certbot","Let's Encrypt"]
categories = ["Let's Encrypt"]
description = "SQL tips"
title = "Let's encrypt and certbot"
author = "Leonidas Simopoulos"
image = "banners/certbot.jpg"
+++


* ##  Obtain certificate from Let's Encrypt using Certbot in STANDALONE mode  

As one line
```
sudo docker run -it --rm -p 443:443 -p 80:80 -v /home/user/someFolder/etc/letsencrypt:/etc/letsencrypt -v /home/user/someFolder/var/lib/letsencrypt:/var/lib/letsencrypt -v /home/user/someFolder/var/log/letsencrypt:/var/log/letsencrypt certbot/certbot certonly --email your.email@email.com --agree-tos --no-eff-email --rsa-key-size 4096 --authenticator standalone -d yourDnsName
```
or with line breaks
```
sudo docker run -it --rm -p 443:443 -p 80:80 \
-v /home/user/someFolder/etc/letsencrypt:/etc/letsencrypt \
-v /home/user/someFolder/var/lib/letsencrypt:/var/lib/letsencrypt \
-v /home/user/someFolder/var/log/letsencrypt:/var/log/letsencrypt \
certbot/certbot certonly  \
--email your.email@email.com --agree-tos --no-eff-email \
--rsa-key-size 4096 --authenticator standalone -d yourDnsName
```

