---
title: WIN使用Miniconda
date: 2017/10/17 20:22:22
tags:
- dev
- Python
categories:
- [开发, Py系列, 环境]
---
## 我应该下载Anaconda还是Miniconda？

选择Anaconda：

* 最先支持conda和python
* 一次性安装150多个常用软件包使python的使用更加方便
* 有充裕的时间和磁盘空间
* 不想每次使用时都需要安装一遍软件包

Anaconda download: [http://continuum.io/downloads](http://continuum.io/downloads)

<!--more-->

选择Miniconda：

* 只想快速使用python和conda命令

Miniconda download: [https://conda.io/miniconda.html](https://conda.io/miniconda.html)

## Miniconda安装

Windows下环境变量配置

```shell
C:\Miniconda3;
C:\Miniconda3\Library\mingw-w64\bin;
C:\Miniconda3\Library\usr\bin;
C:\Miniconda3\Library\bin;
C:\Miniconda3\Scripts;
```

## Miniconda环境管理

```powershell
# 创建一个名为python36的环境，指定Python版本是3.6
conda create --name Python36 python=3.6

# 安装好后，使用activate激活某个环境
activate Python36 

# 激活后，命令行前显示当前环境名称(Python36)

# 此时，再次输入
python --version

# 可以得到Python 3.6.2 :: Continuum Analytics，Inc. 即系统已经切换到了3.6的环境

# 如果想返回root环境，运行
deactivate python36

# 列出所有环境
conda info --envs

# 克隆环境
conda create --name Pythont --clone Python36

# 删除一个已有的环境
conda remove --name python36 --all
```

## Miniconda包管理

```powershell
# 查看当前环境下已安装的包
conda list

# 查看某个指定环境的已安装包
conda list -n Python36

# 查找package信息
conda search numpy

# 安装package
conda install -n Python36 numpy
# 如果不用-n指定环境名称，则被安装在当前活跃环境
# 也可以通过-c指定通过某个channel安装

# 更新package
conda update -n Python36 numpy

# 删除package
conda remove -n Python36 numpy

# 在当前环境下安装anaconda包集合
conda install anaconda

# 结合创建环境的命令，以上操作可以合并为
conda create -n python35 python=3.5 anaconda
# 也可以不用全部安装，根据需求安装自己需要的package即可

# 用pip安装包
# 对于不适用于conda或Anaconda.org的软件包，我们可以选择使用pip安装软件包
pip install see
```

## conda配置

默认情况下不生成`.condarc`文件，会在第一次使用的时候自动在主目录创建。

例：C:\Users\Administrator\\.condarc

conda配置文件可用于更改：

- conda寻找包裹的地方
- 是否以及如何使用代理服务器
- conda在何处列出已知的环境
- 是否使用当前激活的环境名称展示在bash提示符前
- 用户构建的软件包是否应该上传到Anaconda.org
- 是否在新环境中包含默认的软件包或功能
- 等等。

**设置channels** 

例：国内镜像

```powershell
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
```

或修改配置文件`.condarc`

```powershell
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - file:///some/local/directory#为单个环境修改通道
  - defaults
```

注意：对于Windows用户，URL的末尾需要斜杠（/）。

**自动更新conda**

当为True时，每当用户在根环境中更新或安装软件包时，自动更新conda。

当为False时，只有手动更新conda。

默认是`True`。

可以通过编辑`.condarc`文件或使用命令行。

`conda config --set auto_update_conda False`

**操作默认选择yes** 

当要求选择是否以进入下一步是，自动选择yes。比如说下载的时候。

默认是`False`。