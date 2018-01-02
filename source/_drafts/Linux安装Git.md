---
title: Linux安装Git
date: 2017/10/17 20:50:08
tags:
- Linux
---
## 安装步骤

1. 首先更新系统

   * ```shell
     sudo yum update
     ```

<!--more-->

2. 安装依赖包

   * ```shell
     sudo yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel gcc perl-ExtUtils-MakeMaker
     ```

3. 下载git源码并解压缩

   * ```shell
     $ wget https://github.com/git/git/archive/v2.9.4.zip
     $ unzip v2.9.4.zip
     $ cd git-2.9.4
     ```

   * 或者使用tarball解压到指定目录，例/usr/local

     ```shell
     tar -zxvf git-2.9.4.tar.gz -C /usr/local/
     ```

4. 编译安装

   将其安装在指定目录，例/usr/local/git

   ```shell
   sudo make prefix=/usr/local/git all
   sudo make install prefix=/usr/local/git 
   ```

5. 修改并应用环境变量

   ```shell
   sudo vi /etc/profile
   #文件最后一行添加以下内容
   export PATH=/usr/local/git/bin:$PATH
   #命令行使用source使更改生效
   source /etc/profile
   ```

6. 查看git版本

   ```shell
   git --version
   ```

## 设置git

```git
git config --global user.name "Your Name"
git config --global user.email "youremail@domain.com"
```

## 添加SSH Keys

以公钥认证方式访问SSH协议的Git服务器时无需输入口令，而且更安全。（访问HTTP协议的Git服务器时，比如提交修改，每次都需要输入口令。）

1. 创建SSH key

```shell
$ ssh-keygen -t rsa -C "youremail@163.com"
```

系统会提示key的保存位置（一般是~/.ssh目录）和指定口令，保持默认，连续三次回车即可。

2. Copy SSH Key

然后用vim打开该文件，`id_rsa.pub`文件内的内容，粘帖到github帐号管理的添加SSH key界面中。

```shell
vim ~/.ssh/id_rsa.pub
```

3. 添加到GitHub

登录github-> Accounting settings图标-> SSH key-> Add SSH key-> 填写SSH key的名称（可以起一个自己容易区分的），然后将拷贝的`~/.ssh/id_rsa.pub`文件内容粘帖-> add key”按钮添加。

4. 测试

```shell
ssh -T git@github.com
```
WINDOWS下报换行错误

git config --global core.autocrlf false