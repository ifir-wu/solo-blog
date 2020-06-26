title: CentOS下的MySQL安装及配置
date: '2019-09-08 23:41:02'
updated: '2019-09-09 00:13:00'
tags: [MySQL, CentOS, Linux]
permalink: /articles/2019/09/08/1567957261818.html
---
![](https://img.hacpai.com/bing/20181020.jpg?imageView2/1/w/960/h/540/interlace/1/q/100)

## 添加MySQL仓库

CentOS 7的默认yum仓库中并没有MySQL5.7（不建议安装MySQL8），我们需要手动添加，好在MySQL官方提供了仓库的地址。

```bash
# 添加Mysql5.7仓库
$ rpm -ivh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm

# 确认Mysql仓库成功添加
$ yum repolist all | grep mysql | grep enabled
# 不出意外将输入下列信息
# mysql-connectors-community/x86_64  MySQL Connectors Community    enabled:     51
# mysql-tools-community/x86_64       MySQL Tools Community         enabled:     63
# mysql57-community/x86_64           MySQL 5.7 Community Server    enabled:    267
```

## 下载及安装
```bash
# 开始安装Mysql5.7
$ yum -y install mysql-community-server
```

## 启动MySQL
```bash
# 启动Mysql
$ systemctl start mysqld

# 设置系统启动时自动启动
$ systemctl enable mysqld

# 查看启动状态
$ systemctl status mysqld
```

## 安全配置
```bash
# 打印初始密码（CentOS上的root默认密码可以在文件/var/log/mysqld.log找到）
$ cat /var/log/mysqld.log | grep -i 'temporary password'

# 执行下面命令进行安全设置，这个命令会进行设置root密码设置，移除匿名用户，禁止root用户远程连接等
$ mysql_secure_installation
# 安全设置的步骤如下
#    # 1. 输入初始密码（就是上面打印的密码）
#    # 2. 是否更改root密码，如果输入y会要求设置新的密码
#    # 3. 两次设置新密码，建议是大小写，数字和符号的组合，不然会不给通过
#    # 4. 是否删除匿名用户，建议y删除
#    # 5. 是否禁止root远程登录，建议y禁止
#    # 6. 是否删除test数据库，建议y删除
#    # 7. 是否重新加载权限表，建议y重新加载
```

## 设置编码为UTF-8

```bash
$ vim /etc/my.cnf
```

修改 `/etc/my.cnf` 配置文件，在相关节点（没有则自行添加）下添加编码配置，如下：

```
[client]
default-character-set=utf8

[mysql]
default-character-set=utf8

[mysqld]
collation-server = utf8_unicode_ci
init-connect='SET NAMES utf8'
character-set-server = utf8
```

保存退出后，重启MySQL即可

```bash
# 重启MySQL服务
$ systemctl restart mysqld

# 用户名密码进入mysql
$ mysql -uroot -p
```

输入如下命令看编码是否更改

```mysql
mysql> show variables like 'character%';
```


