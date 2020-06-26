title: Cygwin安装和配置
date: '2019-09-09 16:55:56'
updated: '2019-09-09 16:55:56'
tags: [Cygwin]
permalink: /articles/2019/09/09/1568019356852.html
---
![](https://img.hacpai.com/bing/20190901.jpg?imageView2/1/w/960/h/540/interlace/1/q/100)

Cygwin是一个在windows平台上运行的类UNIX模拟环境，是cygnus solutions公司开发的自由软件（该公司开发的著名工具还有eCos，不过现已被Redhat收购）。它对于学习UNIX/Linux操作环境，或者从UNIX到Windows的应用程序移植，或者进行某些特殊的开发工作，尤其是使用GNU工具集在Windows上进行嵌入式系统开发，非常有用。随着嵌入式系统开发在国内日渐流行，越来越多的开发者对Cygwin产生了兴趣。


## Cygwin下载及安装

### 下载

下载地址：

> http://www.cygwin.com/

下载地址截图如下：

![Cygwin官方截图](https://i.loli.net/2018/09/28/5bae02b7a2472.png)

[返回目录](#TOP_jump)

### 安装

1. 安装开始界面。运行`setup-x86_64.exe`程序，出现安装开始画面，直接点`下一步`，如图所示：![安装开始界面](https://i.loli.net/2018/09/28/5bae03c46624c.png)
2. 选择一个下载源。接下来看到三种安装模式：①Install from Internet（直接从Internet安装）；②Download Without Installing（只下载，但不安装）；③Install from Local Directory（从本地安装），默认选择①，这里选择默认选项，并点击`下一步`。![选择一个下载源](https://i.loli.net/2018/09/29/5baf5ed85a607.png)
3. 选择安装路径。接下来选择一个安装路径，最好选择系统盘C以外的盘，如设置安装路径为`D:\cygwin`，然后选择为谁安装Cygwin：①所有用户；②仅仅自己。这里选择①，点击`下一步`。![选择安装路径](https://i.loli.net/2018/09/29/5baf68bc5053b.png)
4. 选择安装包下载路径。这一步用来选择下载的Cygwin组件包的保存位置，一般选择非系统盘C，如选择`E:\CygwinDownloads`，并点击`下一步`。如果当前目录不存在，会提示是否创建该目录，点击`是`即可。![选择下载包安装路径](https://i.loli.net/2018/09/29/5baf6bc7c0811.png)
5. 选择连接至Internet的方式。这一步看到三种连接方式，分别是：①Direct Connection（直接连接）；②Use IE5 Settings（使用IE5设置连接）；③Use HTTP/FTP Proxy（使用HTTP/FTP代理连接）。这里默认选择①，点击`下一步`。![选择连接至Internet的方式](https://i.loli.net/2018/09/29/5baf72b27aac2.png)
6. 选择一个下载源。这里为了获得更快的下载速度，可以在列表中寻找Cygwin中国镜像的地址，如果没有，就在下面手动输入中国镜像地址。再点击`Add`，然后再在列表中选中（按`Ctrl`可以选中多个）。选择完成后，点击`下一步`。可选择或添加的镜像源有如下：①国内中科大：http://mirrors.ustc.edu.cn/cygwin/；②163镜像：http://mirrors.163.com/cygwin/；③清华北大镜像站：https://mirrors.tuna.tsinghua.edu.cn/cygwin/。另外还有其他镜像站，见[附录 国内镜像网站](#附录 国内镜像网站)![选择一个下载源](https://i.loli.net/2018/09/30/5bb04be8b825e.png)
7. <span id = "a_jump" name = "a_jump">选择要下载和安装的组件包</span>。在`View`中选择`Category`，然后在`Search`中输入需要组件包名称，在列表中找到想要安装的组件包，反复点击前面的循环图标可以选择最新版本进行安装。这里首先选择开发工具：①binutils；②gcc-core；③gcc-g++；④gdb；⑤make；⑥mingw64-x86_64-gcc-core；⑦mingw64-x86_64-gcc-g++。然后选择编辑器vim：①gvim；②vim；③vim-doc。最后选择窗口程序支持，用于运行窗口程序：①xinit；②xorg-server；③xorg-server-common。选好之后点击`下一步`。(下图并非原图，而是制作图，主要用来展示所安装的内容)![选择要下载和安装的组件包](https://i.loli.net/2018/10/01/5bb1c2f3568bd.png)
8. 确认需要安装的组件包。用于查看是否和之前的选择是否一致，但是增加了好多相关的组件包，因此查看并不容易，但是一般没问题，直接点击`下一步`即可。![确认需要安装的组件包](https://i.loli.net/2018/10/01/5bb1d2d5a4dc0.png)
9. 安装组件包。接下来就可以看到Cygwin在下载安装相关组件包，耐心等待安装完成即可。![安装组件包](https://i.loli.net/2018/10/01/5bb1d305d879c.png)
10. 创建图标。安装完成后选择是否添加快捷方式：①Create icon on Desktop（创建桌面图标）；②Add icon to Start Menu（添加到开始菜单）。根据需求勾选，然后点击`完成`即可。![创建图标](https://i.loli.net/2018/10/01/5bb1dffd3a1c2.png)
11. 如果安装结束不是提示创建图标，而是提示安装错误，那么可以点击`上一步`尝试重新安装，或者点击`下一步`结束安装。


### 验证是否安装成功

运行cygwin，图标为![Cygwin64 Terminal](https://i.loli.net/2018/10/01/5bb20b68421ee.png)

在弹出的命令行窗口中输入：

> cygcheck -c cygwin

会打印出当前cygwin的版本和运行状态，如果status是OK的话，则cygwin运行正常。

![验证是否安装正确](https://i.loli.net/2018/10/01/5bb20d7dc7efc.png)

然后依次输入以下命令：

> gcc --version
>
> g++ --version
>
> make --version
>
> gdb --version
>
> vim -version
>
> gvim -version

如果都显示相应的版本信息和一些描述信息，则cygwin安装成功。


## 添加环境变量

如果想在windows命令提示符下使用Cygwin，则需要将Cygwin添加到Windows的环境变量。

> 右击->我的电脑——属性（快捷键：`Win+Pause`）——高级系统设置——高级——环境变量

![打开环境变量](https://i.loli.net/2018/10/01/5bb2122a3b01e.png)

> 在“环境变量”窗口中，从“系统变量”中找到“Path”变量，并对其进行编辑，在变量值选项的最后面添加Cygwin下bin路径：`;D:\cygwin64\bin;`，注意前后需要增加分号来区分其他变量值。下图为windows10的操作。

![添加环境变量](https://i.loli.net/2018/10/01/5bb218b058676.png)

添加成功后，就可以打开cmd命令提示符来测试几个Linux命令了。如下图所示，`pwd`和`ls`在Windows命令提示符中可以正常工作了。而且还可以看到`/cygdrive/c`自动被添加到当前目录显示里面了。

![cmd运行linux命令](https://i.loli.net/2018/10/01/5bb21b116350b.png)


## 修改用户目录

启动Cygwin后，其默认的用户主目录是Cygwin安装目录下的用户主目录，即`Cygwin安装目录\home\[UserName]`。如Cygwin安装到`D:\cygwin64`，用户名为`17384`，则默认的用户主目录为`D:\cygwin64\home\17384`。

如不清楚自己的用户主目录路径，可以打开Cygwin Terminal，输入如下指令：

> pwd

则显示用户主目录路径为：

> \home\17384

![默认用户主目录](https://i.loli.net/2018/10/05/5bb756f5246d9.png)

显示的并不是完整路径，而是Linux下的相对路径。如果要获取完整路径，则输入如下命令：

> cygpath -dm "\`pwd\`"
>
> （`pwd`的两边是双引号嵌套反引号（键盘上`1!键`左边的那个``~键`）。

则显示用户主目录路径为：

> D:/cygwin64/home/17384

![用户目录的完整路径](https://i.loli.net/2018/10/05/5bb75b2bbc0ae.png)

如果需要修改该路径，则需要修改环境变量。可以输入如下指令来查看环境变量：

> env

然后寻找变量值为`\home\17384`的变量，该变量名为`HOME`。

![环境变量](https://i.loli.net/2018/10/05/5bb75e073b337.png)

此时只需要修改该变量的变量值，即可更改用户主目录的路径。具体操作如下：

> 打开系统环境变量（具体操作见[添加环境变量](#添加环境变量)）
>
> 在系统变量或者用户变量中新建一个变量
>
> 变量名：HOME
>
> 变量值：E:\Cygwin\home\iFir（或者其他路径）

![添加HOME环境变量](https://i.loli.net/2018/10/05/5bb76164d2256.png)

此时重新打开Cygwin，即可看到用户目录已经更改。

![更新用户目录](https://i.loli.net/2018/10/05/5bb7634e6fabc.png)

## 运行窗口程序

Cygwin默认是无法运行窗口程序的，如需要使用gvim编辑文件，则会提示错误；当写得程序需要打开窗口时，也会提示错误信息。

![运行gvim失败信息](https://i.loli.net/2018/10/01/5bb21cbee7f7c.png)

解决的方法如下：

1. 如果要运行窗口程序，需要安装`x server`。可以选择`xming x server`，也就是`cygwin/x`。最新版的`cygwin/x`已经集成在cygwin的安装程序中，无需另外下载。只需要在安装组件包的时候，添加①xinit；②xorg-server；③xorg-server-common。如果不记得怎么安装，可以回到[7. 选择要下载和安装的组件包](#a_jump)进行查看。

2. 在Cygwin窗口中输入命令：

   > export DISPLAY=:0.0
   >
   > startxwin &

   `startxwin`后面加上&就可以继续在cygwin里面输入命令了，不出意外的话应该能够运行窗口程序了，而且托盘会有`Cygwin/x server:0.0`的图标，并且可以从那退出。

   输入命令后：

   ![启动Cygwin/x server](https://i.loli.net/2018/10/01/5bb2274cf24e3.png)

   托盘显示：

   ![Cygwin/x server图标](https://i.loli.net/2018/10/01/5bb227d42b74f.png)

   如果输入：

   > export DISPLAY=:0.0
   >
   > startxwin &> x-server-log &

   就可以把标准输出和标准错误输出到重定向的文件`x-server-log`中，在cygwin控制台中，就看不到x server的输出信息了。

   ![输出到x-server-log](https://i.loli.net/2018/10/01/5bb2291fe8454.png)

3. <span id = 'b_jump' name = 'b_jump'>如果</span>不希望每次启动都输入代码启动x server，可以把上面两行代码添加在`~/.bashrc`中。

   在Cygwin控制台，进入用户目录`~`，然后查看是否存在`.bashrc`文件，如果有（如果没有，则看[步骤4](#c_jump)），则对其进行修改，具体操作如下：

   > cd ~
   >
   > ls -al
   >
   > gvim .bashrc

   `ls`使用`-al`命令是因为文件名带“.”的文件是隐藏文件，直接使用`ls`命令是无法查看到这些文件的。

   ![查看.bashrc文件](https://i.loli.net/2018/10/06/5bb83f838714e.png)

   如果前面的x server安装正常，并且代码输入正确，那么应该可以看到Gvim正常地打开窗口，并正在对`.bashrc`文件进行修改，此时在该文件最后添加代码保存即可，当然也可以用记事本等文本编辑器修改。

   > export DISPLAY=:0.0
   >
   > startxwin &> x-server-log &

   ![编辑.bashrc](https://i.loli.net/2018/10/06/5bb86ad777450.png)

   退出重启Cygwin，即可看到x server也跟着重新启动了。

4. <span id ="c_jump" name ="c_jump">如果</span>之前修改了用户目录，则新的用户目录下可能不存在`.bashrc`文件。

   ![没有.bashrc文件](https://i.loli.net/2018/10/05/5bb7717d5a85f.png)

   该文件其实在安装时，已经备份在`Cygwin安装目录\etc\skel`目录下。该目录下除了`.bashrc`，还有其他文件，分别为`.bash_profile`，`.inputrc`，`.profile`。

   ![用户配置文件](https://i.loli.net/2018/10/06/5bb8236c0a648.png)

   这些文件是用户配置的重要文件，随着版本（本文Cygwin版本为2.11.1-1）的不同，这些配置文件可能不同。因此只需拷贝`Cygwin安装目录\etc\skel`下的所有文件到更改后的用户目录下即可。

   ![用户配置文件拷贝至用户目录](https://i.loli.net/2018/10/06/5bb824f4db327.png)

   拷贝完成后返回[步骤3](#b_jump)完成接下来的工作。

参考文章;

> 作者：[bovenson](https://home.cnblogs.com/u/bovenson/)
>
> 文章：[cygwin 运行窗口程序](https://www.cnblogs.com/bovenson/p/5118360.html)
