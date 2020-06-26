title: Ubuntu安装gcc，g++，make，gdb
date: '2019-09-10 23:01:27'
updated: '2019-09-10 23:02:39'
tags: [gcc, Ubuntu, C, C++]
permalink: /articles/2019/09/10/1568127686957.html
---
![](https://img.hacpai.com/bing/20190310.jpg?imageView2/1/w/960/h/540/interlace/1/q/100)

1. 更新镜像源

   ```bash
   sudo apt-get update
   ```

2. 安装build-essential

   `build-essential`里包含了gcc，g++，make等常用工具，省去了一个一个包安装的麻烦

   ```bash
   sudo apt-get install build-essential
   ```

   注意这里，如果安装一直失败，暂时发现两种可能：

   + 没有更新为国内镜像，安装速度太慢，导致安装失败
   + 虽然更改为国内镜像，但是镜像与Ubuntu版本不匹配，导致某些包找不到

   解决方法就是正确安装镜像，可以参考本博客里的相关文章

3. 安装gdb

   ```bash
   sudo apt-get install gdb
   ```

4. 检查安装的版本

   ```bash
   gcc -v
   g++ -v
   make -v
   gdb -v
   ```

   Ubuntu18.04安装的版本为

   ```
   gcc version 7.4.0
   GNU Make 4.1
   GNU gdb (Ubuntu 8.1-0ubuntu3) 8.1.0.20180409-git
   ```

   


