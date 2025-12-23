---
title: "Hosting"
description: "ger"
summary: ""
date: 2025-12-19T11:59:19+02:00
lastmod: 2025-12-19T11:59:19+02:00
draft: false
weight: 913
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

## Overview
When you build a website, one of the most important decisions you’ll make is where to host it. Web hosting determines how your site is stored, served to visitors, and kept online. Today, there are many hosting options, ranging from powerful cloud platforms to hosting a site yourself on small hardware like a Raspberry Pi.

### Learning Goals

- Configuring a Web Server(Nginx)
- Configuring an SSL Certificate and Routing.


## 1. Hosting with Cloud Providers

Cloud providers are companies that rent out servers over the internet. Popular options include Linode, Microsoft Azure, AWS, and Google Cloud.

### How it works

- You rent a virtual server (often called a VPS or VM)

- You deploy your website on that server

- The provider handles hardware, networking, and uptime

### Advantages

- High reliability: Data centers have backup power and strong internet connections

- Scalable: Easily upgrade CPU, memory, or storage as your site grows

- Global reach: Many providers let you host close to your users

- Professional tools: Monitoring, backups, and security features are built in

### Disadvantages

- Monthly cost: Even small servers usually cost money

- Learning curve: Platforms like Azure can be complex for beginners

- Overkill for small sites: Simple personal sites may not need this power.


## 2. Self-Hosting on a Raspberry Pi

Self-hosting means running your own server at home. A popular way to do this is using a Raspberry Pi, a small and inexpensive computer.

### How it works

- You install a web server (like Nginx or Apache) on the Raspberry Pi

- You connect it to your home internet

- Your website is served directly from your device

### Advantages

- Very low cost

- Full control over hardware and software

- Great learning experience

- No monthly hosting fees

### Disadvantages

- Lower reliability (power outages, internet downtime)

- Slower performance

- Security responsibility is entirely yours

- More setup and maintenance

## Hosting on a Raspberry Pi

![My photo](/raspberrypi.png)

### Requirements:

- Raspberry Pi 4/5
- Power Source
- SD Card
- Micro HDMI to HDMI Cable
- Computer Screen and Keyboard/Mouse(Optional)

### Raspberry Pi Configuration

- Download the [Raspberry Pi Image](https://www.raspberrypi.com/software/)

- Use the following [Guide](https://www.raspberrypi.com/documentation/computers/getting-started.html#raspberry-pi-imager) to set up the Raspberry Pi.

#### 1. Configure the Web Server:

- `sudo apt install nginx`
- `sudo systemctl start nginx`

#### 2. Running the Node App in the background:
- sudo npm install -g pm2
- pm2 start app.js

#### 3. Setting up an Nginx Proxy
- `sudo vim  /etc/nginx/sites-available/default`
- Replace the location block with the following code:
  ```bash
   location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
  ```
- `sudo systemctl restart nginx`

### Configuring SSL

1. Sign up for a free dynamic domain on [No IP](https://www.noip.com/remote-access).
2. Add the domain to the Nginx config file `/etc/nginx/sites-available/default`
```bash
server_name www.example.com
```
3. Restart Nginx
```bash
sudo systemctl restart nginx
```
4. Install the Let's Encryt Certbot
```bash
sudo apt-get install certbot
```
5. Install the Certbot Nginx Plugin
```bash
sudo apt-get install python3-certbot-nginx
```
6. Run the following command to create the certificate:
```bash
sudo certbot --nginx -d example.com -d www.example.com
```
7. Test the Domain SSL Certificate
```bash
https://www.example.com
```

## 4. Quickstart

{{< callout context="note" title="Github" icon="outline/info-circle" >}}
Clone the [Github Repo](https://github.com/jaimeen12/NodeJS-Passport) and run the following commands:

```bash
git clone https://github.com/jaimeen12/NodeJS-Passport
npm init -y
npm install
node app.js
```

{{< /callout >}}