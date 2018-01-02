---
title: Linux安装JDK
date: 2017/10/17 20:50:36
tags:
- Linux
---
作为[Java](http://lib.csdn.net/base/17)开发人员，在Linux下安装一些开发工具是必备技能，本文以安装jdk为例，详细记录了每一步的操作命令，以供参考。

## 0.下载jdk

登录网址：http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
选择对应jdk版本下载。（可在Windows下下载完成后，通过文件夹共享到Linux上）

<!--more-->

## 1. 登录Linux，切换到root用户

su root 获取root用户权限，当前工作目录不变(需要root密码)


## 2. 在usr目录下建立java安装目录

cd /usr
mkdir java

## 3.将jdk-8u60-linux-x64.tar.gz拷贝到java目录下

mv /mnt/hgfs/linux/jdk-8u60-linux-x64.tar.gz /usr/java/

## 4.解压jdk到当前目录

tar -zxvf jdk-8u60-linux-x64.tar.gz
得到文件夹 jdk1.8.0_60

## 5.安装完毕为他建立一个链接以节省目录长度

(我没用这一步)
ln -s /usr/java/jdk1.8.0_60/ /usr/jdk

## 6.编辑配置文件，配置环境变量

vim /etc/profile
添加如下内容：JAVA_HOME根据实际目录来
exprot JAVA_HOME=/usr/java/jdk1.8.0_60
exprot CLASSPATH=$JAVA_HOME/lib/
exprot PATH=\$PATH:$JAVA_HOME/bin
export PATH JAVA_HOME CLASSPATH

配置环境变量(详细)

vi /etc/profile

export JAVA_HOME=/usr/java/default
export JAVA_BIN=$JAVA_HOME/bin
export PATH=\$PATH:$JAVA_HOME/bin
export CLASSPATH=.:\$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=\$JAVA_HOME/bin:\$JRE_HOME/bin:$PATH

## 7.重启机器或执行命令 ：source /etc/profile

## 8.查看安装情况

java -version

```shell
java version "1.8.0_60"

Java(TM) SE Runtime Environment (build 1.8.0_60-b27)

Java HotSpot(TM) Client VM (build 25.60-b23, mixed mode)
```