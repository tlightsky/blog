---
layout: post
title:  "如何安装mysql服务"
date:   2016-01-16 3:23:57
categories: wordpress mysql linux
---


执行命令`apt-get install mysql-server -y`，
执行过程中需要输入root的初始密码

如果需要从非本地访问数据库，需要做一些修改：

* 修改`/etc/mysql/my.cnf`，注释掉`bind-address            = 127.0.0.1`，然后重启mysql

* 添加一个root的远程账户，代码如下：

```shell script
mysql -u root -p

use mysql;
update user set host='%' where user='root';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
flush privileges;
```


* 备份mysql

```shell script
mysql dump -uroot -p dbname > name.sql
```


* 导入mysql

```shell script
mysql -uroot -p dbname < name.sql
```

* 修密码

```shell script
update user set password=password('123') where user='root' and host='localhost';
```
