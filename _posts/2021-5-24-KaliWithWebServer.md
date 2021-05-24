---
layout:     post
title:      在kali环境下搭建云服务器及网盘
subtitle:   "前情提要: 用树莓派搭建一个小型家庭NAS+网盘"
date:       2021-5-24
author:     XiaoKang00010
header-img: img/404-bg.jpg
catalog: true
tags:
    - Kali Linux
    - Apache
    - php
---


欢迎来到一年一更的xiaokang00010博客!
众所周知，大家都是拿CentOS搭服务器，没人拿debian搭服务器，因此，我先后重装了3次虚拟机系统，最后换回了kali

# 准备工作

需要的东西： KaliLinux_amd64安装iso, 公网服务器, frp, 域名

### 首先先部署公网服务器上的东西

下载github上frp的最新版本，解压。

编辑默认frps.ini,附上我自己的设置
```config
[common]
bind_addr = 0.0.0.0
bind_port = 7000
bind_udp_port = 7001
kcp_bind_port = 7000
dashboard_port = 7500
dashboard_user = admin
dashboard_pwd = nopasswordhere(修改为自己密码)
subdomain_host = nas.xiaokang00010.tk
log_file = ./frps.log
log_level = info
log_max_days = 3
```

启动服务器`setsid ./frps -c frps.ini`，关闭ssh

### 接下来配置本地服务器

配置frpc，此处不再多说

按照上期博客配置服务器环境以及内网samba

**请注意将php7.3全部改为php7.4**

接下来，你就得到了一个私人云盘

成品展示:`nas.xiaokang00010.tk:11451/vfm`