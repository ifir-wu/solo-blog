title: Windows10安装Ubuntu子系统
date: '2019-09-09 16:14:16'
updated: '2019-09-10 08:41:58'
tags: [WSL, Ubuntu, Linux]
permalink: /articles/2019/09/09/1568016856190.html
---
![](https://img.hacpai.com/bing/20181023.jpg?imageView2/1/w/960/h/540/interlace/1/q/100) 

## 准备工作

~~设置——> 更新和安全——> 针对开发人员——> 开发人员模式~~【**貌似也可以不做，如果不能正常进入系统，再设置为开发人员模式**】

控制面板——> 程序——> 程序和功能——> 启用或关闭 Windows 功能——> 适用于 Linux 的 Windows 子系统——> 确定 （然后重启）

## 下载并安装 Ubuntu

在应用商店中搜索 Ubuntu，点击获取进行下载及安装，安装完毕点击启动会打开 bash 命令行提示我们设置用户名（常用的不具有 root 权限的用户）和密码。我这里设置的是：

> 用户名：ubuntu
>
> 密码：123456

完成之后就可以随意折腾你的 linux 系统了。万一我们不小心把子系统折腾崩了，只需要像应用软件一样卸载掉再重新安装就可以了，有需要的话我们甚至还可以安装多个不同版本的子系统，简直不要太方便。

子系统存放在 `C:\用户\用户名\`下的隐藏目录中。点击顶部的查看选项卡——> 隐藏的项目，可以看到 AppData 文件夹。子系统所在目录为：

> C:\ 用户 \ 用户名 \ AppData \ Local \ Packages \ CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc \ LocalState\rootfs

查看当前系统版本：

```
lsb_release -a
```

## 子系统相关问题

ubuntu怎么切换到root用户？【然而一般并不这样做，一般通过sudo来获得管理员权限】

> 我们都知道使用su root命令，去切换到root权限，此时会提示输入密码，可是怎么也输不对，提示“Authentication failure”，
>
> 此时有两种情况一个是真的是密码错了，另一种就是刚安装好的Linux系统，没有给root设置密码。
>
> 首先给root设置密码：
>
> > sudo passwd root
>
> 输入密码，并确认密码。
>
> 然后重新输入：
>
> > su root
>
> 并输入密码即可切换为root权限了。

如何重启Ubuntu子系统，而不重启windows？

> 管理员身份运行cmd，在cmd中输入：
>
> >net stop LxssManager
> >
> >net start LxssManager

win10和子系统的文件系统交互：

> 在 win10 环境下访问 Ubuntu 文件系统的 home 目录：
>
> > C:\Users\xxx\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs\home\xxx
>
> 在 Ubuntu 系统下访问 win10 的 home 目录：
>
> >  /mnt/c/Users/xxx
>
> 在 WSL 环境下可以创建一个访问 win10 的快捷方式
>
> > ln -s /mnt/c/Users/xxx ~/win10 
>
> 在 ubuntu 下通过下面的命令直接进入 win10 的 home 目录
>
> > cd win10
