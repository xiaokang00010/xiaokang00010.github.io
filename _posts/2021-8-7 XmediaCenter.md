---
layout:     post
title:      组建自己的媒体中心！XmediaCenter实用教程！
subtitle:   "一种替代网易云和哔哩哔哩的方法"
date:       2021-8-7
author:     XiaoKang00010
header-img: img/404-bg.jpg
catalog: true
tags:
    - Server
    - XmediaCenter
    - 整活
---


欢迎来到一年一更的xiaokang00010博客!
<s>这个up居然一年更了两次博客，一定是被人绑架了（雾）</s>

# 前言
众所周知，最近在我的服务器上又整了个新活，拿python3和flask写了个简简单单的媒体中心小项目来练练手。<br>

至于Xlang,可能等这个项目发布了stable release再更新。<br>

那怎么使用呢？

# 安装
- Requires: Python 3.9 or higher , MediaInfo

## Configure your XmediaCenter

首先，把git仓库clone下来
```bash
git clone https://github.com.cnpmjs.org/leadsoft-ware/XmediaCenter
```

接下来进入到项目的目录下执行
```
make init
```

但这还没完，这只是安装了最基本的依赖。
```bash
pip3 install pymediainfo you-get
```
如果您正在使用的是Linux系统，可能还需要设置path
```bash
export PATH=~/.local/bin:$PATH
```

Windows用户：

修改项目中的`core/plugins/BilibiliVideosDownloader/main.py`中
```python
fp = os.popen('~/.usr/local/bin/you-get ' + url + ' -o "' + path + '"','r')
```
一行中的`~/.usr/local/bin/you-get`改为`you-get`
可能还要自行设置path

## Configure PyMediaInfo

众所周知，PyMediaInfo安装完之后他的MediaInfo是没有安装完的。此时WINDOWS用户要自行补充MediaInfo的dll到python的根目录内，而Linux用户则需要安装两个deb包.

此处参考:
[Windows上PyMediaInfo安装](https://www.cnblogs.com/fengbo1113/p/10225920.html)

Linux平台我并没有现成的教程，所以现在是Linux的安装方法：<br>
下载这几个deb包：
[libmediainfo0v5](https://mediaarea.net/download/binary/libmediainfo0/21.03/libmediainfo0v5_21.03-1_amd64.Debian_10.deb)
[libzen0v5](https://mediaarea.net/download/binary/libzen0/0.4.39/libzen0v5_0.4.39-1_amd64.Debian_10.deb)
[MediaInfo](https://mediaarea.net/download/binary/mediainfo/21.03/mediainfo_21.03-1_amd64.Debian_10.deb)<br>
然后拿apt安装。

## 运行！
接下来到项目根目录运行`make run`<br>
然后访问`127.0.0.1:12345`如果你看见
```
Hello everyone, this is the default page of XmediaCenter.

Server currently working.Thanks for using.Good luck.
By xiaokang00010!
```
恭喜你🎉！你搭建完成了！<br>
主页:`http://localhost:12345/main`<br>
默认账号:`admin`<br>
默认密码:`114514`<br>
如需增加用户，新建一个python文件，将XmediaCenter.py中的内容复制过来，然后删掉app.run一行
写上app.create_account('用户名','密码')
然后运行即可.