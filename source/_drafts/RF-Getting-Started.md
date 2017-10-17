---
title: RF Getting Started
tags:
- test
---
## 安装配置

###基本配置

**python2.7** :

目前robot framework的工具和Lib对python3.x版本支持不是很完善，基本上使用python2.7版本。

**wxPython** :

安装RIDE所必须的库，注意版本对应，目前最好的支持是[wxpython2.8.12.1](https://sourceforge.net/projects/wxpython/files/wxPython/2.8.12.1/) ，使用pip安装的最新版不能兼容，且记得选unicode版本。

<!--more-->

**robot framework** :

直接用pip安装挺方便的`pip install robotframework`

**robotframework-ride** :

图形管理界面，同样pip安装`pip install robotframework-ride `

**robotframework-selenium2library** :

装了这个库，基本就可以跑UI测试了`pip install robotframework-selenium2library`



###备注

若安装RobotFramework-ride没有自动创建桌面快捷方式，我们要么命令行走起，要么自己搞个快捷方式。**命令行** ：

`WIN+r` 输入`cmd`回车进入命令行，cd到对应目录下，例：`cd C:\Python27\Scripts`，然后敲`python ride.py`来打开。若是配置好了环境变量，直接命令行输入`ride.py` 就启动起来了。

如果ride启动失败了，可以用管理员的身份试一试。

**快捷方式** ：

桌面鼠标右键，选择创建快捷方式，在弹窗中选择`pythonw.exe`再在其后输入`-c "from robotide import main;main()`"，这时输入框中的内容应该类似这样`C:\Python27\pythonw.exe -c "from robotide import main; main()"` 。点击下一步，改个你喜欢的名字，我比较喜欢正规点的"RIDE"，这样完成后就能从桌面进入了。

同样，若是启动失败了。右键快捷方式选择属性，在高级中勾选`用管理员的身份运行` 。

若安装wxPython失败，查看一下版本是否是对应的版本，我这边因为是通过conda安装的，所以安装wxPython的时候一直提示没有找到python2.7的注册信息。这是因为在安装miniconda时没有勾选将miniconda以python2.7默认注册到系统。



```shell
pip install -U robotframework-databaselibrary
```
