---
layout: post
tags:
     - Raspbian
     - RaspberryPi
     - 树莓派
     - samba
date: 2020-07-04
title: 用树莓派搭建一个小型家庭NAS+网盘
subtitle: 树莓派牛批！
header-img: img/404-bg.jpg
---

啊这...爷又回来更新啦！

# 准备工作 

## 安装raspbian
下载地址： `https://www.raspberrypi.org/downloads/raspberry-pi-os/`

将下载来的软件用Win32DiskImager写入到SD卡内

将SD卡插入树莓派

开机！

## 更换apt软件源

输入`sudo apt edit-sources`并键入树莓派的密码

选择vim并打开

将里面的网址的开头替换成`http://mirrors.163.com`

然后保存

# 安装软件

## 安装互联网核心 **这里我用了apache**

```
sudo apt install apache2
sudo apt install php7.3-fpm php7.3-curl php7.3-gd php7.3-mbstring php7.3-mysql php7.3-imap php7.3-opcache php7.3-xml php7.3-xmlrpc php7.3-zip uw-mailutils php-pear -y
```

## 然后安装NAS软件 **这里使用samba**

```
sudo apt install samba
```

## 安装线上文件管理器
这里用了vfm
[安装教程及介绍](http://blog.liyuans.com/archives/veno-file-manager.html/comment-page-1?replyTo=2938)

# 后续工作

重启树莓派 : `init 6`

用树莓派的浏览器打开`localhost/vfm`

默认账号：`admin`
默认密码：`password`

设置网址：`localhost/vfm/vfm-admin`

## 设置samba

配置samba
```
sudo vim /etc/samba/smb.conf
```

```
#共享名称
[share]
#评论、标题
　　comment = test
#分享目录
　　path = /var/www/html/vfm/uploads
#可写权限
　　writable = yes
#可读权限
　　browable = yes
```

samba用户权限配置

`sudo sambapasswd -a pi`（当前已经存在的用户名，这里就是pi了）

