title: Anaconda基本命令
date: '2019-09-10 20:11:51'
updated: '2019-09-10 20:44:28'
tags: [Anaconda]
permalink: /articles/2019/09/10/1568117511750.html
---
![](https://img.hacpai.com/bing/20190315.jpg?imageView2/1/w/960/h/540/interlace/1/q/100)

## 基本命令

1. 查看conda 版本

   ```bash
   conda --version
   # 或
   conda -V
   ```

2. 查看conda帮助

   ```bash
   conda --help
   # 或
   conda -h
   ```

3. 更新Anaconda

   ```bash
   conda update anaconda
   ```

4. 更新conda

   ```bash
   conda update conda
   ```

## 环境管理

1. 新建虚拟环境

   ```bash
   # 创建包含指定python版本的环境
   conda create --name <env_name> python=x.x
   
   # 创建包含指定python版本的环境，并安装相关包
   conda create --name <env_name> python=x.x <package1_name> <package2_name> ...
   
   # 创建包含指定python版本的环境，并安装Anaconda包集合
   conda create -n <env_name> python=x.x anaconda
   ```

   比如：

   - `conda create –name python2 python=2.7`为创建一个名为“python2”的环境，环境中安装2.7版本的python。
   - `conda create -n conda-test python=3.6 numpy pandas`，即创建一个名为“conda-test ”的环境，环境中安装3.6版本的python，同时一同安装numpy和pandas。

2. 切换conda环境

   ```bash
   # Windows下
   activate <env_name>
   
   # Linux & Mac下
   source activate <env_name>
   ```

3. 退出虚拟环境返回默认环境

   ```bash
   # Windows下
   deactivate <env_name>
   
   # Linux & Mac下
   source deactivate <env_name>
   
   # 或者不写环境
   deactivate
   source deactivate
   ```

4. 显示安装过的所有虚拟环境

   用户安装的环境都会被放在目录`~/anaconda/envs`下，可以使用下列命令列出所有环境，其中当前被激活的环境会显示有一个星号或者括号。

   ```bash
   conda info --envs
   # 或
   conda info -e
   # 或
   conda env list
   ```

5. 复制环境

   ```
   conda create --name <new_env_name> --clone <copied_env_name>
   # copied_env_name为被复制的环境名
   ```

6. 删除环境

   ```bash
   conda remove --name <env_name> --all
   ```

## 包管理

1. 查找包

   ```bash
   # 精确查找
   conda search --full-name <package_name>
   
   # 模糊查找
   conda search <package_name>
   ```

2. 获取已安装的包信息

   ```bash
   # 查看当前环境的包信息
   conda list
   
   # 查看指定环境的包信息
   conda list -n <env_name>
   ```

3. 安装包

   ```bash
   # 在当前环境安装包
   conda install <package_name>
   
   # 在指定环境安装包
   conda install --name <env_name> <package_name>
   
   # 指定安装包的版本
   conda install --name <env_name> <package_name>=X.X.X
   # 如：
   conda install --name <env_name> django=2.0.6
   
   # 在当前环境下安装anaconda包集合
   conda install anaconda
   ```

4. 更新包

   ```bash
   # 更新当前环境的包
   conda update <package_name>
   
   # 更新指定环境的包
   conda update -n <env_name> <package_name>
   ```

5. 删除包

   ```bash
   # 删除当前环境的包
   conda remove <package_name>
   
   # 删除指定环境的包
   conda remove -n <env_name> <package_name>
   ```

6. 使用pip安装

   如果conda无法安装，也可以使用pip安装

   ```bash
   pip install <package_name>
   ```






