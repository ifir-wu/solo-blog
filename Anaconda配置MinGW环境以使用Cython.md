title: Anaconda配置MinGW环境，以使用Cython
date: '2019-09-09 09:15:34'
updated: '2019-09-09 09:19:05'
tags: [Cython, MinGW, Anaconda]
permalink: /articles/2019/09/09/1567991734272.html
---
![](https://img.hacpai.com/bing/20180724.jpg?imageView2/1/w/960/h/540/interlace/1/q/100) 

## 安装Anaconda

安装Anaconda较为简单，网上有很多教程，这里就不详细介绍了，注意安装时勾选自动配置环境变量。



## 更改镜像

这里遇到了很多坑，有些教程不完善，导致更改了镜像反而不能使用，让我一度以为是我的电脑问题，后来百度“清华 anaconda”，查询到如下网址：

> [Anaconda| 镜像站使用帮助 | 清华大学开源软件镜像站](https://www.baidu.com/link?url=BWuRrmmlw_fa-cpBre12UCsLdX2CiTTxMZhwjkp0bFKdl9KNqitbIgpNHG7anLtgGLMzweBxkOv2LnD3y4CD4a&wd=&eqid=8adedb64000022ac000000045d2dbca7)

才知道应该这样更改（说是清华镜像挂了，改中科大镜像的，感觉还是一个样，都不能用）：

运行以下命令：

```powershell
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes
```

此时会在用户文件夹（C:/user/用户名）下出现`.condarc`，用记事本打开该文件，删除包含`default`一行，应该会得到如下文件：

```
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
show_channel_urls: true
```

保存后，输入命令：

```powershell
conda info
```

即可查看是否已经更改镜像源。



## 更新conda

conda在安装其他包时可能会提示如下的错误信息：

```powershell
WARNING: The conda.compat module is deprecated and will be removed in a future release.
```

说明要升级conda，此时输入如下命令：

```powershell
conda update conda
```

更新conda即可，这里要求镜像必须能用，否则会导致出错，无法更新。如果能更新，就多更新几次，使得没有包可安装为止。

这时在安装其他包时可能还会出现其他警告信息：

```powershell
WARNING conda. base. context: use_only_tar_bz2(632): Conda is constrained to only using the old. tar. bz2 file format becaus e you have conda-build installed, and it is <3.18.3. Update or remove conda-build to get smaller downloads and faster e xtractions.
```

说明`conda-build`的版本过低，此时输入如下命令即可：

```powershell
conda update conda-build
```



## 安装MinGW以搭建C/C++环境

这里也是我遇到最多坑的地方，更不可思议的是，居然找不到解决方案，都要哭了。

重要的事情说三遍**不要自己下载MinGW搭建环境！！不要自己下载MinGW搭建环境！！不要自己下载MinGW搭建环境！！**

Anaconda之前版本默认有MinGW环境，最近版本不再提供MinGW环境，但是通过conda可以直接安装该环境，只需要执行如下命令：

```powershell
conda install libpython m2w64-toolchain -c msys2
```

这里感谢知乎的《[10 分钟入门 Cython](https://zhuanlan.zhihu.com/p/49573586)》提供了答案。

然后配置MinGW至环境变量，在PATH变量中添加：

> D:\ProgramData\Anaconda3\Library\mingw-w64\bin
>
> D:\ProgramData\Anaconda3\Library\mingw-w64\x86_64-w64-mingw32\lib

如果是windows7，应该在变量前后加上分号。

文章《[Python 的 Cython 在 Windows 环境下的部署安装](https://my.oschina.net/u/1024349/blog/120375)》（当前版本貌似不用做了）还提到：

要在路径`D:\ProgramData\Anaconda3\Lib\distutils`下创建`distutils.cfg`文件，并在文件中写入：

```
[build]          
compiler=mingw32 
```

同时在当前目录下找到`cygwinccompiler.py`，将里面出现的字符串`-mno-cygwin`的全部删掉。

但是我发现貌似现在的版本已经不用在完成这些步骤了。



## 安装MinGW的坑（可以不看）

需要注意的是，anaconda有两种安装MinGW的方式，一种是上面的安装方法（我们称为方法一），一种是输入如下命令进行安装（我们称为方法二）：

```powershell
conda install mingw libpython
```

但两种结果是完全不一样的。

方法一安装的位置在：

> D:\ProgramData\Anaconda3\Library\mingw-w64

方法二安装的位置在：

> D:\ProgramData\Anaconda3\MinGW

并且安装的版本也不一样。

方法一安装的是：5.3.0版本，方法二安装的是：4.7.0版本

然而只有方法一能够正常使用Cython，方法二和自己安装的MinGW都会导致如下错误：

```powershell
CompileError: command 'XXXX路径下的\\gcc.exe' failed with exit status 1
```

据说是因为版本过高？但安装了低版本也不行。网上也没有关于该问题的正确解答。《[Cython官方文档](http://docs.cython.org/en/latest/)》里有个[附录：在Windows上安装MinGW](http://docs.cython.org/en/latest/src/tutorial/appendix.html)，附录下的一个链接[CythonExtensionsOnWindows](https://github.com/cython/cython/wiki/CythonExtensionsOnWindows)特别强调不要使用MinGW，要用`Microsoft Visual C++ Compiler for Python`，然而网上搜索到的MSVC只支持2.7版本，对于3.X版本的目前好像尚未发布。因为这个文档导致我差点放弃MinGW环境，进而放弃使用Cython。

记录方法二是因为文章《[win10 安装 anaconda+mingw+theano+keras 及配置经验](https://blog.csdn.net/xiaoxiaogh/article/details/79188446)》提到这种方法，或许安装theano和keras就需要这样安装MinGW呢，虽然现在还不知道theano和keras是怎么用，但记录下来以防以后出现问题。
