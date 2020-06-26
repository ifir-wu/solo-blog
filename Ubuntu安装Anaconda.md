title: Ubuntu安装Anaconda
date: '2019-09-10 19:38:45'
updated: '2019-09-25 19:32:24'
tags: [Anaconda, Python, Ubuntu, Linux]
permalink: /articles/2019/09/10/1568115524895.html
---
![](https://img.hacpai.com/bing/20190318.jpg?imageView2/1/w/960/h/540/interlace/1/q/100)

## 删除自带的Python

输入`python3`或者`python`，如果存在python，则需要先卸载，卸载命令如下：

1、卸载python3

```bash
sudo apt-get remove python3
```

2、卸载python3及其依赖

```bash
sudo apt-get remove --auto-remove python3
```

3、清除python3

```bash
# 注意：此方法卸载python比较彻底，所以适合更换python版本时使用。
#      对于既想完全卸载python，又无法接受完全卸载后某些python组件无法使用的童鞋，请慎重！！
sudo apt-get purge python3
# or
sudo apt-get purge --auto-remove python3
```

## 下载

去[官方地址](https://www.anaconda.com/download/#linux)下载好对应的安装包。

如这里选择`Linux`下的`Python 3.7 version`，点击`64-Bit (x86) Installer (517 MB)`即可开始下载

下载后将得到`Anaconda3-2019.07-Linux-x86_64.sh`安装文件

## 安装

切换到`Anaconda3-2019.07-Linux-x86_64.sh`所在目录，运行下列命令即可开始安装。

```bash
bash Anaconda3-2019.07-Linux-x86_64.sh
```

安装过程中看到

> Welcome to Anaconda3 5.2.0. In order to continue the installation process, please review the license agreement.
> Please, press ENTER to continue.

即提示查看审核许可证协议。这时候一直按`enter`键，直到看到下列提示：

> Do you accept the license terms? [yes|no]

询问是否接受许可证条款，直接输入`yes`，然后按`enter`键进入下一步。

接下来会提示安装地址：

> Anaconda3 will now be installed into this location:
>
> /home/username/anaconda3
>
> + Press ENTER to confirm the location
> + Press CTRL-C to abort the installation
> + Or specify a different location below

建议默认，即按enter继续下一步，注意这里按ctrl + c 直接会终止安装。

接下来先等待安装即可。当看到`Thank you for installing Anaconda3!` 表示安装成功。

## 配置环境变量

### Bash下的环境变量配置

安装完默认是配置好环境变量的，输入`conda -V`可以查看版本信息，若提示`command not found: conda`，则说明环境变量没生效，输入下面的代码更新环境变量即可。

```bash
source ~/.bashrc
```

如果更新了环境变量还是不可用，那可能是环境变量没有配置正确，只能手动添加环境变量了。

  修改`.basrc`文件

  ```bash
  # 切换到用户目录下
  cd ~
  # 编辑.bashrc文件
  vim .bashrc
  ```

  在末尾添加：

```bash
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/ifir/anaconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/ifir/anaconda3/etc/profile.d/conda.sh" ]; then                                                               . "/home/ifir/anaconda3/etc/profile.d/conda.sh"
    else
        export PATH="/home/ifir/anaconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

保存退出后，更新环境变量

```bash
source ~/.bashrc
```

### zsh下的环境变量配置

如果你还使用`zsh`，那么也应该将环境变量加入到`.zshrc`文件中：

修改`.zshrc`文件

```bash
# 切换到用户目录下
cd ~
# 编辑.bashrc文件
vim .zshrc
```

在末尾添加：

```bash
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/ifir/anaconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/ifir/anaconda3/etc/profile.d/conda.sh" ]; then                                                               . "/home/ifir/anaconda3/etc/profile.d/conda.sh"
    else
        export PATH="/home/ifir/anaconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

保存退出后，更新环境变量

```bash
source ~/.zshrc
```

## 运行

上面的事情都做好后，输入`python`就能开始写python了。
