title: Anaconda更改镜像源及更新
date: '2019-09-10 19:50:03'
updated: '2019-09-11 20:29:37'
tags: [Anaconda, Python]
permalink: /articles/2019/09/10/1568116203158.html
---
![](https://img.hacpai.com/bing/20180624.jpg?imageView2/1/w/960/h/540/interlace/1/q/100)

## 更改镜像

这里遇到了很多坑，有些教程不完善，导致更改了镜像反而不能使用，让我一度以为是我的电脑问题，后来百度“清华 anaconda”，查询到如下网址：

> [Anaconda| 镜像站使用帮助 | 清华大学开源软件镜像站](https://www.baidu.com/link?url=BWuRrmmlw_fa-cpBre12UCsLdX2CiTTxMZhwjkp0bFKdl9KNqitbIgpNHG7anLtgGLMzweBxkOv2LnD3y4CD4a&wd=&eqid=8adedb64000022ac000000045d2dbca7)

才知道应该这样更改（说是清华镜像挂了，改中科大镜像的，感觉还是一个样，都不能用，其实清华镜像已经恢复了）：

建议直接修改用户文件夹（windows系统为`C:/user/用户名`，Linux系统为`~/`）下的`.condarc`，文件，用记事本或vim打开，删除其中的全部内容，到[Anaconda| 镜像站使用帮助 | 清华大学开源软件镜像站](https://www.baidu.com/link?url=BWuRrmmlw_fa-cpBre12UCsLdX2CiTTxMZhwjkp0bFKdl9KNqitbIgpNHG7anLtgGLMzweBxkOv2LnD3y4CD4a&wd=&eqid=8adedb64000022ac000000045d2dbca7)里复制镜像，然后更改即可。

因为据我多次安装发现，这个镜像貌似会变，导致有时候莫名其妙下载失败，如果发现下载失败，就看看镜像是不是更新了。

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



