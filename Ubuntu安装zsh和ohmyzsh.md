title: Ubuntu安装zsh和oh-my-zsh
date: '2019-09-09 16:34:47'
updated: '2019-09-11 20:33:39'
tags: [oh-my-zsh, zsh, Ubuntu, Linux]
permalink: /articles/2019/09/09/1568018087531.html
---
![](https://img.hacpai.com/bing/20181216.jpg?imageView2/1/w/960/h/540/interlace/1/q/100)

本文是在windows10下的子系统进行的操作，但在Ubuntu虚拟机或Ubuntu系统中的操作也是大同小异。

## 相关命令

1. 查看当前shell

> echo $SHELL

2. 查看安装的所有shell

> cat /etc/shells

## 安装zsh

> sudo apt-get install zsh

查看zsh的版本号：

> zsh --version

## 安装oh-my-zsh的坑（可跳过）

在这里遇到了很大的坑，一直找不到解决方案，导致一度想放弃。但好在经过不懈努力，不断尝试，最终得到解决，特记录下来，以防忘记。

首先可能需要安装wget和git，命令为：

> sudo apt-get install wget git

然后根据[oh-my-zsh](https://ohmyz.sh/)官网的提示的安装命令进行安装：

> sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
>
> sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"

但发现并不可以，提示错误信息如下

> curl: (7) Failed to connect to raw.github.com port 443: Operation timed out

又或者不断尝试连接。



**第一次尝试解决**

查了网上的资料：

> [让你的终端个性起来~ oh-my-zsh 简单安装教程](https://www.jianshu.com/p/300827734b69)
>
> [Windows10 终端优化方案：Ubuntu 子系统 + cmder+oh-my-zsh](https://zhuanlan.zhihu.com/p/34152045)
>
> [win10 安装 oh my zsh 和 window git bash 设置别名提高效率](https://www.jianshu.com/p/97f33b7fac80?utm_source=oschina-app)
>
> [Zsh和Oh My Zsh的安装配置](https://www.wangzhanshi.com/programming/centos/6539.html)
>
> [win10创建Ubuntu16.04子系统，安装常用软件以及图形界面（包括win10远程桌面连接Ubuntu）](https://blog.csdn.net/li528405176/article/details/82263534)

又有如下的安装命令：

> sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
>
> sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
>
> wget --no-check-certificate https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh

但都无济于事，视乎只有我一个遇到这种问题一样，网上的资料并没有记录关于这种错误的解决方法，好不容易找到相同问题的文章：

> [下不动，这玩意有镜像么 oh my zsh](https://segmentfault.com/q/1010000014144697)

但并没有得到有用的结果。



**第二次尝试解决**

我开始寻求其他的解决方案，比如使用antigen，这是查阅到的相关资料：

> [Linux下antigen的安装与用法](https://ywnz.com/linuxrj/3059.html)
>
> [antigen的GitHub](https://github.com/zsh-users/antigen)

antigen是zsh的包管理器，貌似通过它可以很方便的安装zsh的相关插件，包括oh-my-zsh。找到antigen的安装命令：

> curl -L git.io/antigen > antigen.zsh

然而却有遇到了一样的问题，同样安装失败，同样无法连接某个网址，同样无法连接的是raw.githubusercontent.com和raw.github.com网址，貌似就是过不了这个坎。



**第三次尝试解决**

参考资料：

> [安装 homebrew 报错 curl: (7) Failed to connect to raw.githubusercontent.com port 443: Operation](https://www.jianshu.com/p/68efabd2e32b)

说是先尝试用浏览器打开命令中的连接，如果打不开就要检查自己的网络。经过尝试，果然无法打开 https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh网页，但我确定，网络是完好的，因为我用手机4G网络也尝试过了。

只能说这个网址有问题，但要怎么解决呢？怎么连接这个网页呢？没有答案。。。



**第四次尝试解决**

考虑到整了一下午的Ubuntu，是不是被我搞坏了，导致安装东西就会出错，所以我决定卸载了重装。然后重复尝试后还是不行。



**最后一次尝试解决**

为了弄一个完美的终端，我也尝试过babun，它被评价为一个自带oh-my-zsh的终端神器，然而在安装它的时候，也出现了一个无法解决的问题，那就是`babun check`出现失败，说是无法连接代理，无法更新。但是找了好久，网上只有一个安装教程，而且教程里没有出现任何问题，似乎只有我一个人遇到这种问题一样，但是我的电脑是刚刚重装系统不久，还没开始玩机呢。

于是我弃坑来整Ubuntu子系统，本以为应该不会再出现这种不能解决的问题吧，毕竟资料相对多点，结果还是天真，就在我快要放弃的时候，突然想到是不是因为GitHub被限速的原因呢？因为之前弄过这个，所以很快百度：

> GitHub提速

找到了这篇文章

> [GitHub 轻松提速教程](https://www.cnblogs.com/LyShark/p/10574755.html)

就是访问：https://www.ipaddress.com/ 网址

依次获取以下三个网址的 IP

> github.com
> github.global.ssl.fastly.net
> codeload.github.com

然后将获取到的IP和上述域名写在hosts文件中，即将下面的文本写在hosts文件末尾。

> 192.30.253.113 github.com
> 151.101.25.194 github.global.ssl.fastly.net
> 192.30.253.121 codeload.github.com

hosts文件在`C:\Windows\System32\drivers\etc\hosts`下，需要管理员身份才能修改，可以尝试使用notepad++修改，当保存时会提示是否用管理员身份保存该文件。我是通过火绒浏览器的更改hosts功能进行修改的。

改完后刷新DNS，即在cmd中输入：

> ipconfig /flushdns

值得一提的是，子系统中也有一个hosts文件【在etc目录下】，但当执行上述命令后，该文件会自动同步windows的hosts文件，可见windows10对子系统做了很好的适配。

然而这样做后依然没有效果，网站依旧无法访问。突然看到这篇文章：

> [github上不去解决方法](https://blog.csdn.net/qq_25973779/article/details/80030181)

在下面找到了raw.githubusercontent.com网址，难道也要把这个网址放在hosts文件中？抱着尝试的态度，我到[https://www.ipaddress.com/](https://www.ipaddress.com/)查阅了无法进入的这两个网址的IP，得到如下结果：

> 151.101.184.133 raw.githubusercontent.com
> 151.101.184.133 raw.github.com

然后把它放在hosts文件的末尾，保存，并通过`ipconfig /flushdns`刷新DNS。然后尝试在浏览器查看https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh，居然能够访问了！

神仙保佑，希望安装的时候不要出问题，重新运行命令：

> sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

幸喜若狂的时候到了，安装成功了！感动到哭。

记录下可能会用到的GitHub域名IP，以防以后要用到：

> 192.30.253.113 github.com
> 192.30.253.119 gist.github.com
> 151.101.184.133 raw.github.com
> 140.82.113.10 codeload.github.com
> 151.101.185.194 github.global.ssl.fastly.net
> 151.101.184.133 raw.githubusercontent.com
> 151.101.184.133 gist.githubusercontent.com
> 151.101.184.133 cloud.githubusercontent.com
> 151.101.184.133 camo.githubusercontent.com
> 151.101.184.133 avatars0.githubusercontent.com
> 151.101.184.133 avatars1.githubusercontent.com
> 151.101.184.133 avatars2.githubusercontent.com
> 151.101.184.133 avatars3.githubusercontent.com
> 151.101.184.133 avatars4.githubusercontent.com
> 151.101.184.133 avatars5.githubusercontent.com
> 151.101.184.133 avatars6.githubusercontent.com
> 151.101.184.133 avatars7.githubusercontent.com
> 151.101.184.133 avatars8.githubusercontent.com
> 151.101.184.133 avatars9.githubusercontent.com
> 151.101.184.133 avatars10.githubusercontent.com
> 151.101.184.133 avatars11.githubusercontent.com
> ~~#151.101.100.133 assets-cdn.github.com【查询不到IP】~~

然而这种方式视乎并不稳定，经常失败，最好的办法是代理。

## 安装oh-my-zsh

总结上面，安装oh-my-zsh需要先修改hosts文件（因为国内访问GitHub受到限速，所以更改hosts文件可以提速，但是最有效的方法还是代理）。
hosts文件在：
Windows：`C:\Windows\System32\drivers\etc\hosts`下，需要管理员身份才能修改。
Ubuntu：`/etc/hosts`下，使用`sudo vim /etc/hosts`修改。
如果Ubuntu是Win10的子系统，只需修改Win10的hosts文件，Ubuntu的hosts文件会自动更新。

修改的内容如下：

> 192.30.253.113 github.com
> 192.30.253.119 gist.github.com
> 151.101.184.133 raw.github.com
> 140.82.113.10 codeload.github.com
> 151.101.185.194 github.global.ssl.fastly.net
> 151.101.184.133 raw.githubusercontent.com
> 151.101.184.133 gist.githubusercontent.com
> 151.101.184.133 cloud.githubusercontent.com
> 151.101.184.133 camo.githubusercontent.com
> 151.101.184.133 avatars0.githubusercontent.com
> 151.101.184.133 avatars1.githubusercontent.com
> 151.101.184.133 avatars2.githubusercontent.com
> 151.101.184.133 avatars3.githubusercontent.com
> 151.101.184.133 avatars4.githubusercontent.com
> 151.101.184.133 avatars5.githubusercontent.com
> 151.101.184.133 avatars6.githubusercontent.com
> 151.101.184.133 avatars7.githubusercontent.com
> 151.101.184.133 avatars8.githubusercontent.com
> 151.101.184.133 avatars9.githubusercontent.com
> 151.101.184.133 avatars10.githubusercontent.com
> 151.101.184.133 avatars11.githubusercontent.com

改完后刷新DNS，即在cmd中输入：

> ipconfig /flushdns

安装wget和git，命令为：

> sudo apt-get install wget git

根据[oh-my-zsh](https://ohmyz.sh/)官网的提示的安装命令进行安装：

> sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
>
> sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"

完成。

如果[https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh](https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)网址无法访问，可以尝试连接手机热点，或者删除在hosts文件中新增的github，多试几次，应该都能成功。

但其实最好的办法就是代理了。

## 设置为默认的shell

> chsh -s /bin/zsh

## 设置主题及安装使用插件

可以参考网址：

> [Oh-My-Zsh主题集汇总](https://birdteam.net/131798)
>
> [猿内功：终端 + oh-my-zsh 漂亮配色、实用插件](https://www.jianshu.com/p/0d32ed87c8a8)

选择自己喜欢的主题，然后：

> vim ~/.zshrc
>
> #编写配置文件
>
> ZSH_THEME="gnzh"
>
> #将引号内的内容改为效果图上对应的单词就行了，如果设置成random会随机哦

注意：这里千万不要用windows的记事本，notepad++等windows下的软件进入子系统的目录中去修改`.zshrc`文件，会导致该文件损坏，原因不详，导致我又重装了一次子系统。。。所以为了避免文件损坏，最好备份一份，并使用子系统的文本编辑器修改。

当然还可以修改属于自己的主题：

> [其他：oh-my-zsh终端用户名屏蔽设置](https://blog.csdn.net/z3512498/article/details/51245853)
>
> [iTerm2+oh-my-zsh 之 隐藏用户名信息](https://www.jianshu.com/p/7e43d2ae8fac)
>
> [Ubuntu 18.04 on Windows 10 更改 Oh-My-Zsh agnoster 主题下的目录背景色](https://www.cnblogs.com/Ricky81317/p/9062590.html)


