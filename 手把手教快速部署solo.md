title: 手把手教快速部署solo
date: '2019-09-07 21:46:03'
updated: '2019-09-25 14:36:30'
tags: [Solo]
permalink: /solo
---
![](https://img.hacpai.com/bing/20190829.jpg?imageView2/1/w/960/h/540/interlace/1/q/100) 

## 前期准备

### 购买服务器

1. 进入[阿里云官网](https://www.aliyun.com/)，并登录；

2. 搜索框输入“学生服务器”（24岁及以下，或学生认证后），点击搜索；
   ![阿里云.png](https://img.hacpai.com/file/2019/09/阿里云-132f3383.png)

3. 点击“学生云服务器”

   ![阿里云学生云服务器.png](https://img.hacpai.com/file/2019/09/阿里云学生云服务器-d1e1bbce.png)

4. 选择轻量服务器，并购买

   ![轻量服务器.png](https://img.hacpai.com/file/2019/09/轻量服务器-ad81e0a3.png)

5. 支付，如果是学生这里应该是114一年。

   ![购买轻量服务器.png](https://img.hacpai.com/file/2019/09/购买轻量服务器-a3467144.png)

### 申请域名

1. 进入[阿里云官网](https://www.aliyun.com/)，并登录；

2. 进入[万网](https://wanwang.aliyun.com/)，并搜索喜欢的域名；

   ![万网.png](https://img.hacpai.com/file/2019/09/万网-11866b51.png)

3. 选择自己喜欢的域名，并点击“加入清单”；

   ![域名加入清单.png](https://img.hacpai.com/file/2019/09/域名加入清单-5d5557a0.png)

4. 购买域名

   ![购买域名.png](https://img.hacpai.com/file/2019/09/购买域名-7af80ee5.png)

### 域名备案

1. 下载阿里云APP，并登录
2. 点击“控制台”，找到“网站备案”，即可快速备案
3. 耐心等待15天左右

域名证书下载方式：

1. 进入[阿里云控制台](https://homenew.console.aliyun.com/)，点击左上角三杠，选择“域名”

   ![控制台域名.png](https://img.hacpai.com/file/2019/09/控制台域名-e27d3fff.png)

2. 点击域名

   ![点击域名.png](https://img.hacpai.com/file/2019/09/点击域名-645695ee.png)

3. 点击左边的“域名证书下载”

   ![域名证书下载.png](https://img.hacpai.com/file/2019/09/域名证书下载-a2efe98d.png)

### 开启SSL证书（无需备案成功）

1. 进入[阿里云控制台](https://homenew.console.aliyun.com/)，点击左上角三杠，选择“域名”

   ![控制台域名.png](https://img.hacpai.com/file/2019/09/控制台域名-4f44627c.png)

2. 点击域名

   ![点击域名.png](https://img.hacpai.com/file/2019/09/点击域名-561d95fc.png)

3. 点击左边的“基本信息”，然后找到下面的“免费开启SSL证书”

   ![免费开启SSL证书.png](https://img.hacpai.com/file/2019/09/免费开启SSL证书-95e6ff09.png)

4. 购买免费的证书（因为这里已经买过了，所以没有免费证书这一项），如果买了，就点击上面的返回证书列表

   ![返回证书列表.png](https://img.hacpai.com/file/2019/09/返回证书列表-dcc72d0c.png)

5. 点击“申请”

   ![申请SSL.png](https://img.hacpai.com/file/2019/09/申请SSL-a6d5f6b7.png)

6. 填写信息，注意这里的“证书绑定域名”要带上“www”，不然可能会审核失败

   ![SSL证书信息填写.png](https://img.hacpai.com/file/2019/09/SSL证书信息填写-e5db30b1.png)

7. 验证信息并提交审核，然后没几分钟就审核通过了。

   ![SSL证书信息验证.png](https://img.hacpai.com/file/2019/09/SSL证书信息验证-26110c30.png)

### 进入服务器控制台

1. 进入[阿里云控制台](https://homenew.console.aliyun.com/)，点击左上角三杠，点击“产品与服务”，找到“轻量应用服务器”并点击

   ![进入轻量应用服务器.png](https://img.hacpai.com/file/2019/09/进入轻量应用服务器-1264207e.png)

2. 点击服务器右上角的图标，点击“详情”

   ![服务器详情.png](https://img.hacpai.com/file/2019/09/服务器详情-1dce116b.png)

3. 在里面可以找到公网IP，设置密码，设置域名（因为之前设置没有留下照片，所以请自行设置）

## 安装相关工具

### 本地安装Xshell和Xftp工具

下载工具

1. 到[官网的免费授权页面](https://www.netsarang.com/zh/free-for-home-school/)输入姓名和邮箱，点击确定，软件将以邮件的形式发到邮箱
2. 下载后，傻瓜式安装

登录服务器

1. 在会话窗口中输入服务器的公网IP，用户名和密码，建议点击记住密码，方便下次登录。

2. 进入Xshell，首先更新yum镜像，不然下载龟速，配置方法见下个章节。

3. Xshell在登录上之后 Centos 系统可能会出现一个警告（也可忽略该警告）：

   > WARNING! The remote SSH server rejected X11 forwarding request.

   解决办法：

   ```bash
   # 安装相关包
   $ yum -y install xorg-x11-xauth
   ```

   但是仍然有问题，报出这样的问题

    > /usr/bin/xauth: file /root/.Xauthority does not exist

   `/etc/ssh/sshd_config`文件中,找到下面参数，刚开始是被注释的，改完保存退出。

    ```
    AllowAgentForwarding //设置为yes（去掉注释），但要求下面这个配置也为true
    X11Forwarding //设置为yes（默认应该都是的）
    ```

   至此问题就完美解决了。接下来的安装都是在Xshell和Xftp上操作。

### 更新yum镜像

```bash
# 备份
$ mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup

# 下载新的CentOS-Base.repo 到/etc/yum.repos.d/
$ wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo

# 生成缓存
$ yum makecache

# 将yum包更新到最新
$ yum update

# 用久了可能yum下载时速度很慢，会不停的换mirrors，可能到了最后还会安装失败
# 这时候我们可以考虑清楚缓存并更新
$ yum clean all
$ yum makecache
$ yum update
# 然后重新安装命令即可
```

### 安装JDK

1. 本地打开浏览器，输入连接：https://www.oracle.com/java/technologies/jdk8-downloads.html

2. 找到`jdk-8u221-linux-x64.tar.gz`点击下载即可（可能要登录，自己注册一个账号吧）

3. 服务器端输入以下命令，新建一个文件夹用来存放java

   ```bash
   # 进入/usr/local目录
   $ cd /usr/local
   
   # 创建/usr/local/java目录
   $ mkdir java
   
   # 进入java目录
   $ cd java
   ```

4. 用Xftp将`jdk-8u221-linux-x64.tar.gz`上传到`/usr/local/java`目录

5. 解压安装

   ```bash
   # 解压
   $ tar -xzvf jdk-8u171-linux-x64.tar.gz
   
   # 重命名
   $ mv jdk1.8.0_171 jdk1.8
   ```

6. 配置系统环境变量

   ```bash
   $ vim /etc/profile
   ```

   在文件最后输入：

   ```bash
   # jdk
   export JAVA_HOME=/usr/local/java/jdk1.8
   export JRE_HOME=/usr/local/java/jdk1.8/jre
   export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
   export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
   ```

   使配置生效

   ```bash
   $ source /etc/profile
   ```

7. 验证jdk是否安装成功

   ```bash
   # 查看java版本
   $ java -version
   
   # 查看javac版本
   $ javac -version
   ```

### 安装MySQL

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

# 开始安装Mysql5.7
$ yum -y install mysql-community-server

# 启动Mysql
$ systemctl start mysqld

# 设置系统启动时自动启动
$ systemctl enable mysqld

# 查看启动状态
$ systemctl status mysqld

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

设置数据库编码为utf8

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

### 安装Docker

``` bash
# 确保 yum 包更新到最新
$ yum update
  
# 安装 Docker（本文直接用着这个，没有安装最新稳定版）
$ yum -y install docker
# 或者安装最新稳定版 Docker（需要先设置 yum 源）
$ yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
$ yum install docker-ce
  
# 启动 Docker 后台服务
$ service docker start
  
# 验证安装是否成功,如果跳出版本信息则成功（我这里输出的是1.13.1版本）
$ docker version
# 测试运行 hello-world（出现 hello world 就证明安装正常了）
$ docker run hello-world
  
# 加入开机启动
$ systemctl enable docker
# 提示如下即添加成功：
# Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.
```

## 安装NGINX

```bash
# 使用 yum 安装 nginx
$ yum install nginx

# 开启 nginx 服务
$ service nginx start

# 查看 nginx 状态
$ systemctl status nginx
```

## 十分钟用IP快速部署solo

### 前置条件

1. JDK1.8安装在本地
2. MySQL安装在服务器本地，而不是安装在Docker
3. 如果没有域名，或者域名还没有备案

### 创建数据库

```bash
# 用户名密码进入mysql
$ mysql -uroot -p
```

```mysql
# 创建数据库(数据库名:solo;字符集utf8mb4;排序规则utf8mb4_general_ci)
mysql> create database solo DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
# 出现Query OK, 1 row affected (0.00 sec)表示成功

# 退出数据库
mysql> exit
```

### 挂载皮肤文件夹

为了使用[更多的皮肤](https://solo.b3log.org/)，可以新建一个皮肤文件夹，之后挂载该文件夹即可：

```bash
# 下载git
$ yum install git

# 新建目录
$ mkdir -p /usr/local/solo

# 进入solo目录
$ cd /usr/local/solo

# 下载官方皮肤到solo目录(/usr/local/solo/)下
$ git clone https://github.com/b3log/solo-skins.git skins

# 进入skins目录(/usr/local/solo/skins/)中
$ cd skins

# 删除不必要的文件
$ rm -rf README.md

# 下载其他皮肤到skins目录下，格式为 git clone github皮肤地址 皮肤名字
$ git clone https://github.com/zjhch123/solo-skin-emiya emiya
```

记住我们的皮肤目录为`/usr/local/solo/skins/`，下面要用到。

### 挂载Markdowns目录

为了将写好的markdown文件直接导入，可以新建一个markdowns文件夹，之后挂载该文件夹即可：

```bash
# 切换到/usr/local/solo/目录
$ cd /usr/local/solo

# 新建markdowns目录
$ mkdir markdowns
```

记住我们的markdowns目录为`/usr/local/solo/markdowns/`，下面要用到。


### 新建docker-restart.sh文件

为了方便，我们直接新建一个`docker-restart.sh`文件，输入如下命令：

```bash
# 切换到/usr/local/solo/目录
$ cd /usr/local/solo/

# 新建docker-restart.sh文件
$ vim docker-restart.sh
```

然后在`docker-restart.sh`(`/usr/local/solo/docker-restart.sh`)文件中输入如下命令（注意需要修改的地方）：

```bash
#!/bin/bash

# Solo docker 更新重启脚本
# 1. 请注意修改参数：
#    # a. 修改数据库的相关参数
#    #    # --env RUNTIME_DB="____"    # 如果用的是H2，就填 "H2"，否则不改
#    #    # --env JDBC_USERNAME="____" # 数据库用户名
#    #    # --env JDBC_PASSWORD="____" # 数据库密码
#    #    # --env JDBC_DRIVER="____"   # 如果数据库是H2，则改成 "org.h2.Driver"
#    #    # --env JDBC_URL="____"      # 如果数据库是H2，则改成
#    #    #                            # "jdbc:h2:/opt/solo/h2/db;MODE=MYSQL"
#    # b. 修改server_scheme            # 如果域名备案且进行了SSL认证，则修改为”https"
#    # c. 修改server_host              # 填写自己的公网IP或域名（不带端口号）
#    # d. 挂载皮肤目录                  # 找到下面这行代码，将/usr/local/solo/skins/改成自己的皮肤目录
#    #    #                            # --volume /usr/local/solo/skins/:/opt/solo/skins/
#    # e. 挂载markdowns目录             # 找到下面这行代码，将/usr/local/solo/skins/改成自己的皮肤目录
#    #    #                            # --volume /usr/local/solo/markdowns/:/opt/solo/markdowns/:rw
# 2. 可将该脚本加入 crontab，每日凌晨运行来实现自动更新

echo "正在获取solo的最新镜像..."
docker pull b3log/solo &> /dev/null

echo "正在检查solo容器是否正在运行..."
# docker ps    # 查看正在运行的容器
# grep solo    # 查找是否存在solo关键词
# &> /dev/null # 重定向标准输出和错误到/dev/null，这个文件比较特殊，传给它的东西都丢弃
docker ps | grep solo &> /dev/null

# 判断上次查询命令的结果是否为0，1为无匹配，0为有匹配
if [ $? -eq 0 ]
then
    echo "正在停止运行solo容器..."
    docker stop solo &> /dev/null
fi

echo "正在检查是否存在solo容器..."
# docker ps -a       # 查看所有容器，包括停止运行的容器
docker ps -a | grep solo &> /dev/null

while [ $? -eq 0 ]
do
    echo "正在删除solo容器..."
    # docker rm solo # 删除solo容器
    # 2>&1           # 将标准错误和标准输出的结果直接输出
    # var=$(...)     # 将输出的结果赋值给var
    var=$(docker rm solo 2>&1)

    # 再次检查是否存在solo容器，如果还存在，则说明有进程占用
    docker ps -a | grep solo &> /dev/null

    if [ $? -eq 0 ]
    then
        echo "发现有占用的进程，正在杀死这些进程..."
        # 获取solo的id
        # echo ${var}     # 输出var的值
        # grep -E -o exp  # 将exp用正则匹配(-E)的方法去匹配前面输出的字符串
        #                 # 并只输出匹配的内容(-o)
        # awk '{print substr($2,12)}'
        #                 # 输出上面的结果的子字符串，从第12个字符开始
        # var=$(...)      # 将上面的结果存在var变量中，此时会得到solo的id
        var=$( echo ${var} | grep -E -o "filesystem [a-zA-Z0-9]+" | awk '{print substr($2,12)}' )
        # 查找占用solo的进程号，并杀掉
        # grep "$var" /proc/*/mountinfo
        #                 # 获取占用solo的进程信息
        # grep -E -o "proc/[0-9]+" | awk '{print substr($1,6)}'
        #                 # 获取这些进程的id
        # xargs kill -9   # 杀掉这些进程
        grep "$var" /proc/*/mountinfo | grep -E -o "proc/[0-9]+" | awk '{print substr($1,6)}' | xargs kill -9
    fi

    echo "正在检查是否存在solo容器..."
    docker ps -a | grep solo &> /dev/null
done

echo "正在新建并运行solo容器..."
# 各参数说明：
#    # --name solo             # 命名该容器为solo
#    # --network=host          # 使用主机网络模式来连接主机上的MySQL
#    # --env RUNTIME_DB=...    # 使用MYSQL数据库
#    # --env JDBC_USERNAME=... # 数据库的用户名
#    # --env JDBC_PASSWORD=... # 数据库的密码
#    # --env JDBC_DRIVER=...   # 数据库的驱动
#    # --env JDBC_URL=...      # 数据库的URL，数据库名，字符编码等信息
#    # --volume ~/skins/:/opt/solo/skins/  
#    #                         # 挂载皮肤文件，前面的~/skins/为自己的皮肤目录
#    # --volume ~/markdowns/:/opt/solo/markdowns/:rw  
#    #                         # 挂载markdowns文件，前面的~/markdowns/为自己的皮肤目录
#    # --listen_port=8080      # 监听的端口
#    # --server_scheme=http    # 最终访问的协议，
#    #                         # 可以使用http或https（需要申请SSL，并通过反代服务启动）
#    # --server_host=...       # 最终访问的域名（如果有）或IP，不带端口号
#    # --server_port=          # 最终访问的端口，为空则使用默认端口
#    #                         # （http:80, https:443）
docker run --detach --name solo --network=host \
    --env RUNTIME_DB="MYSQL" \
    --env JDBC_USERNAME="root" \
    --env JDBC_PASSWORD="123456" \
    --env JDBC_DRIVER="com.mysql.cj.jdbc.Driver" \
    --env JDBC_URL="jdbc:mysql://127.0.0.1:3306/solo?useUnicode=yes&characterEncoding=UTF-8&useSSL=false&serverTimezone=UTC" \
    --volume /usr/local/solo/skins/:/opt/solo/skins/ \
    --volume /usr/local/solo/markdowns/:/opt/solo/markdowns/:rw \
    b3log/solo --listen_port=8080 --server_scheme=http --server_host=***.***.***.*** --server_port= \
    &> /dev/null

sleep 2

echo "正在停止nginx服务..."
service nginx stop &> /dev/null
sleep 1

echo "正在重载nginx配置文件..."
service nginx reload &> /dev/null
sleep 1

echo "正在启动nginx服务..."
service nginx start &> /dev/null
sleep 1

echo "正在输出运行中容器的信息和nginx服务启动的状态..."
docker ps
systemctl status nginx
```

### NGINX安装配置

```bash
# 切换到/usr/local/solo/目录
$ cd /usr/local/solo/

# 新建一个 blog.conf 配置文件:
$ touch blog.conf

# 进入 blog.conf 编辑状态
$ vim blog.conf
```

在`blog.conf`(`/usr/local/solo/blog.conf`)输入如下内容（注意修改server_name为自己的公网IP）：

```bash
# nginx配置文件
# 请注意修改参数：
#    # 修改server_name              # 修改为自己的域名

server {
  listen 80;
  server_name ***.***.***.***;

  location / {
      proxy_pass http://127.0.0.1:8080;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
  }
}
```

保存并退出，然后修改`nginx.conf`(`/etc/nginx/nginx.conf`)文件，输入：

```bash
$ vim /etc/nginx/nginx.conf
```

在`nginx.conf`(`/etc/nginx/nginx.conf`)的`http`块下，插入一行：

```
include /usr/local/solo/*.conf;
```

修改后应该差不多是这样的（添加在下面节选代码的第10行）：

```
... ...
# Load dynamic modules. See /usr/share/nginx/README.dynamic.
include /usr/share/nginx/modules/*.conf;

events {
    worker_connections 1024;
}

http {
    include /usr/local/solo/*.conf;
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;
... ...
```

保存后退出。

然后输入下面命令检查配置文件是否正确：

```bash
# 检查配置文件是否正确
nginx -t
```

### 开放防火墙

1. CentOS中开放防火墙

   ```bash
   # 查看防火墙状态
   $ firewall-cmd --state
   
   # 开启防火墙
   $ systemctl start firewalld.service
   
   # 设置开机自启：
   $ systemctl enable firewalld.service
   
   # 开放相关端口
   firewall-cmd --zone=public --add-port=80/tcp --permanent
   firewall-cmd --zone=public --add-port=443/tcp --permanent
   firewall-cmd --zone=public --add-port=8080/tcp --permanent
   # 命令含义
   #    # --zone             # 作用域
   #    # --add-port=80/tcp  # 添加端口，格式为：端口/通讯协议
   #    # --permanent        # 永久生效，没有此参数重启后失效
   
   # 重启防火墙：
   $ systemctl restart firewalld.service
   
   # 检查防火墙状态是否打开
   $ firewall-cmd --state
   
   # 查看防火墙设置开机自启是否成功：
   $ systemctl is-enabled firewalld.service;echo $?
   
   # 查看开启的所有端口
   $ firewall-cmd --list-ports
   ```

2. 阿里云控制台开放防火墙

   浏览器进入[阿里云控制台](https://homenew.console.aliyun.com/)，然后进入轻量服务器

   ![防火墙.png](https://img.hacpai.com/file/2019/09/防火墙-55642c57.png)

### 一条命令下载、更新、运行solo

```bash
$ sh /usr/local/solo/docker-restart.sh
```

此时在浏览器输入服务器的公网IP地址（无需端口号）就可以访问博客了。

### 加入crontab 以定时更新

```bash
#  查看crond状态
$ systemctl status crond

# 设为开机启动
$ systemctl enable crond 

# 启动crond服务
$ systemctl start crond 

# 编辑crontab以加入定时任务（通过crontab -e命令，shell内的部分命令会失败，所以采用以下方法）
vim /etc/crontab
```

在文件中添加如下命令，表示root用户每天凌晨3点执行docker-restart.sh，并将标准错误和标准输出重定向到docker-restart.log文件，方便查看。

```bash
00 3 * * * root sh /usr/local/solo/docker-restart.sh >> /usr/local/solo/docker-restart.log 2>&1
```

最后的文件应该是这样的：

```bash
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root

# For details see man 4 crontabs

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name  command to be executed

00 3 * * * root sh /usr/local/solo/docker-restart.sh >> /usr/local/solo/docker-restart.log 2>&1
```

保存退出即可。




## 三步更新为域名访问

### 前置条件

1. 进行了上述操作。
2. 域名已备案。

### 更新docker-restart.sh文件

用vim打开`docker-restart.sh`(`/usr/local/solo/docker-restart.sh`)文件
```bash
# 打开docker-restart.sh文件
$ vim /usr/local/solo/docker-restart.sh
```

找到`b3log/solo`那一行，将`--server_host`改为域名

```bash
    b3log/solo --listen_port=8080 --server_scheme=http --server_host=www.****.com --server_port= \
```

保存退出即可

### 更新blog.conf文件

用vim打开`blog.conf`(`/usr/local/solo/blog.conf`)文件

```bash
# 打开blog.conf文件
$ vim /etc/nginx/conf.d/blog.conf
```

找到`server_name `那一行，将IP改为域名。

```bash
    server_name www.****.com;
```

### 重启solo

```bash
$ sh /usr/local/solo/docker-restart.sh
```



## 四步添加SSL证书

### 前置条件

1. 进行了上述操作。
2. 域名已备案。
3. 购买了SSL证书，并审核通过。
4. 注意防火墙开放443端口。

### 下载SSL证书

在阿里云控制台中找到“SSL证书”。

![SSL证书](https://img.hacpai.com/file/2019/09/image-938f273a.png)

然后点击“下载”，选择“Nginx”

![下载SSL证书](https://img.hacpai.com/file/2019/09/image-dec9b9a4.png)

![Nginx证书](https://img.hacpai.com/file/2019/09/image-d7b225cc.png)

下载完后将得到一个压缩包`一串数字_域名_nginx.zip`，解压得到`一串数字_域名.pem`和`一串数字_域名.key`两个文件。通过Xftp将其拷贝到`/usr/local/solo/`目录下。

![拷贝证书](https://img.hacpai.com/file/2019/09/image-e61ef545.png)

### 更新docker-restart.sh文件

用vim打开`docker-restart.sh`(`/usr/local/solo/docker-restart.sh`)文件

```bash
# 打开docker-restart.sh文件
$ vim /usr/local/solo/docker-restart.sh
```

找到`b3log/solo`那一行，将`--server_scheme`改为`https`

```bash
    b3log/solo --listen_port=8080 --server_scheme=https --server_host=www.****.com --server_port= \
```

保存退出即可

### 更新blog.conf文件

用vim打开`blog.conf`(`/usr/local/solo/blog.conf`)文件

```bash
# 打开blog.conf文件
$ vim /usr/local/solo/blog.conf
```

更改文件内容为

```bash
# nginx配置文件
# 请注意修改参数：
#    # a. 修改server_name              # 修改为自己的域名，共两处
#    # b. 修改ssl_certificate          # 修改为自己的ssl证书的pem文件的路径
#    # c. 修改ssl_certificate_key      # 修改为自己的ssl证书的key文件的路径

#server {
#    listen 80;
#    # 公网ip或域名
#    server_name www.****.com;
#    location / {
#        proxy_pass http://127.0.0.1:8080;
#        proxy_set_header Host $host;
#        proxy_set_header X-Real-IP $remote_addr;
#        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
#    }
#}

# 将80端口强制转为访问443端口
server {
  listen       80;
  server_name www.****.com;
  return 301 https://$server_name$request_uri;
}
# 设置443端口
server {
    listen 443 ssl http2;
    server_name www.****.com;
    ssl on;
    # 添加SSL证书
    ssl_certificate /usr/local/solo/一串数字_域名.pem;
    ssl_certificate_key /usr/local/solo/一串数字_域名.key;
    ssl_session_timeout 5m;
    ssl_protocols TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    ssl_ciphers "EECDH+CHACHA20:EECDH+CHACHA20-draft:EECDH+AES128:RSA+AES128:EECDH+AES256:RSA+AES256:EECDH+3DES:RSA+3DES:!MD5";
    ssl_session_cache builtin:1000 shared:SSL:10m;
    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

### 重启solo

```bash
$ sh /usr/local/solo/docker-restart.sh
```


