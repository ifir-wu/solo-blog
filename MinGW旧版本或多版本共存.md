title: MinGW旧版本或多版本共存
date: '2019-09-09 16:03:23'
updated: '2019-09-09 16:03:23'
tags: [MinGW]
permalink: /articles/2019/09/09/1568016203816.html
---
![](https://img.hacpai.com/bing/20190215.jpg?imageView2/1/w/960/h/540/interlace/1/q/100)

可参考《[MinGW with gcc4.8.1的手动安装](https://blog.51cto.com/zhanggx/1305040)》和官方文档《[HOWTO Install the MinGW (GCC) Compiler Suite](http://www.mingw.org/wiki/InstallationHOWTOforMinGW)》，具体步骤如下：

> 1. 在[这里](https://sourceforge.net/projects/mingw/files/)下载下列安装包
>
> > 必须的。除gcc-core可以选择自己喜欢的版本外，其余的都可以选择最新版
> >
> > - binutils ([bin](http://sourceforge.net/projects/mingw/files/MinGW/Base/binutils/binutils-2.23.2-1/binutils-2.23.2-1-mingw32-bin.tar.lzma/))
> > - mingw-runtime ([dev](http://sourceforge.net/projects/mingw/files/MinGW/Base/mingw-rt/mingwrt-3.20/mingwrt-3.20-2-mingw32-dev.tar.lzma/) and [dll](http://sourceforge.net/projects/mingw/files/MinGW/Base/mingw-rt/mingwrt-3.20/mingwrt-3.20-2-mingw32-dll.tar.lzma/))
> > - [w32api](http://sourceforge.net/projects/mingw/files/MinGW/Base/w32api/w32api-3.17/w32api-3.17-2-mingw32-dev.tar.lzma/)
> > - Required runtime libraries for GCC:
> >   - mpc ([dll](http://sourceforge.net/projects/mingw/files/MinGW/Base/mpc/mpc-1.0.1-2/mpc-1.0.1-2-mingw32-dll.tar.lzma/))
> >   - mpfr ([dll](http://sourceforge.net/projects/mingw/files/MinGW/Base/mpfr/mpfr-3.1.2-2/mpfr-3.1.2-2-mingw32-dll.tar.lzma/))
> >   - gmp ([dll](http://sourceforge.net/projects/mingw/files/MinGW/Base/gmp/gmp-5.1.2/gmp-5.1.2-1-mingw32-dll.tar.lzma/))
> >   - pthreads ([dev](http://sourceforge.net/projects/mingw/files/MinGW/Base/pthreads-w32/pthreads-w32-2.9.1/pthreads-w32-2.9.1-1-mingw32-dev.tar.lzma/) and [dll](http://sourceforge.net/projects/mingw/files/MinGW/Base/pthreads-w32/pthreads-w32-2.9.1/pthreads-w32-2.9.1-1-mingw32-dll.tar.lzma/))
> >   - iconv ([dll](http://sourceforge.net/projects/mingw/files/MinGW/Base/libiconv/libiconv-1.14-3/libiconv-1.14-3-mingw32-dll.tar.lzma/))
> >   - [zlib](http://sourceforge.net/projects/mingw/files/MinGW/Base/zlib/zlib-1.2.8/zlib-1.2.8-1-mingw32-dll.tar.lzma/)
> >   - [gettext](http://sourceforge.net/projects/mingw/files/MinGW/Base/gettext/gettext-0.18.3.1-1/gettext-0.18.3.1-1-mingw32-dll.tar.lzma/)
> > - gcc-core ([bin](http://sourceforge.net/projects/mingw/files/MinGW/Base/gcc/Version4/gcc-4.8.1-4/gcc-core-4.8.1-4-mingw32-bin.tar.lzma/) and [dev](http://sourceforge.net/projects/mingw/files/MinGW/Base/gcc/Version4/gcc-4.8.1-4/gcc-core-4.8.1-4-mingw32-dev.tar.lzma/) and [dll](http://sourceforge.net/projects/mingw/files/MinGW/Base/gcc/Version4/gcc-4.8.1-4/gcc-core-4.8.1-4-mingw32-dll.tar.lzma/))               <-----编译C必须安装
> > - gcc-c++ ([bin](http://sourceforge.net/projects/mingw/files/MinGW/Base/gcc/Version4/gcc-4.8.1-4/gcc-c%2B%2B-4.8.1-4-mingw32-bin.tar.lzma/) and [dev](http://sourceforge.net/projects/mingw/files/MinGW/Base/gcc/Version4/gcc-4.8.1-4/gcc-c%2B%2B-4.8.1-4-mingw32-dev.tar.lzma/) and [dll](http://sourceforge.net/projects/mingw/files/MinGW/Base/gcc/Version4/gcc-4.8.1-4/gcc-c%2B%2B-4.8.1-4-mingw32-dll.tar.lzma/)) for C++   <-----编译C++必须安装，和gcc-core必须为同一版本
> >
> > 可选的。可以安装最新版。
> >
> > - [mingw-gdb](http://sourceforge.net/projects/mingw/files/MinGW/Extension/gdb/gdb-7.6.1-1/gdb-7.6.1-1-mingw32-bin.tar.lzma/) 和 [libexpat](http://sourceforge.net/projects/mingw/files/MinGW/Extension/expat/expat-2.1.0-1/expat-2.1.0-1-mingw32-dll.tar.lzma/)                            <-----用于调试
> > - [mingw32-make](http://sourceforge.net/projects/mingw/files/MinGW/Extension/make/make-3.82.90-cvs/make-3.82.90-2-mingw32-cvs-20120902-bin.tar.lzma/)                                       <-----make，组织C项目，方便编译运行C项目
> > - [mingw-utils](http://sourceforge.net/projects/mingw/files/MinGW/Extension/mingw-utils/mingw-utils-0.4-1/mingw-utils-0.4-1-mingw32-bin.tar.lzma/) for MinGW Utilities
> > - [msysDTK](http://downloads.sourceforge.net/mingw/msysDTK-1.0.1.exe) for Unix-style developer toolkit
> > - [MSYS](http://sourceforge.net/projects/mingw/files/MSYS/Base/msys-core/msys-1.0.11/MSYS-1.0.11.exe/) for Unix-style commands and shell. (See the [MSYS](http://www.mingw.org/wiki/MSYS) page for installation instructions.)
> >
> > - 将[gcc](http://sourceforge.net/projects/mingw/files/MinGW/Base/gcc/Version4/gcc-4.8.1-4/gcc-4.8.1-4-mingw32-lang.tar.lzma/)，[binutils](http://sourceforge.net/projects/mingw/files/MinGW/Base/binutils/binutils-2.23.2-1/binutils-2.23.2-1-mingw32-lang.tar.lzma/)，[gdb](http://sourceforge.net/projects/mingw/files/MinGW/Extension/gdb/gdb-7.6.1-1/gdb-7.6.1-1-mingw32-lang.tar.lzma/)和[make](http://sourceforge.net/projects/mingw/files/MinGW/Extension/make/make-3.82.90-cvs/make-3.82.90-2-mingw32-cvs-20120902-lang.tar.lzma/)消息翻译成英语以外的语言   <-----版本需对应
> > - [gcc-core](http://sourceforge.net/projects/mingw/files/MinGW/Base/gcc/Version4/gcc-4.8.1-4/gcc-core-4.8.1-4-mingw32-doc.tar.lzma/)，[gcc-c ++](http://sourceforge.net/projects/mingw/files/MinGW/Base/gcc/Version4/gcc-4.8.1-4/gcc-c%2B%2B-4.8.1-4-mingw32-doc.tar.lzma/)和[gcc-fortran的](http://sourceforge.net/projects/mingw/files/MinGW/Base/gcc/Version4/gcc-4.8.1-4/gcc-fortran-4.8.1-4-mingw32-doc.tar.lzma/)文档   <----版本需对应
>
> 2. 将文件解压缩到如`C:\ MinGW`的目录中
> 3. 添加`C:\MinGW\bin; `到PATH环境变量中

