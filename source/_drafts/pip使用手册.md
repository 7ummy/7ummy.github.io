---
title: pip使用手册
date: 2017/10/17 20:01:08
tags:
- dev
- Python
categories:
- [开发, Py系列, pip]
---
## pip安装包

```shell
$ pip install SomePackage
  [...]
  Successfully installed SomePackage
```

<!--more-->

安装本地包

```shell
$ pip install SomePackage-1.0-py2.py3-none-any.whl
  [...]
  Successfully installed SomePackage
```

版本控制

 ```shell
$ pip install SomePackage            # latest version
$ pip install SomePackage==1.0.4     # specific version
$ pip install 'SomePackage>=1.0.4'     # minimum version
 ```

通过wheel安装

```shell
pip install SomePackage-1.0-py2.py3-none-any.whl
```

本地安装wheel包
```bash
#To build wheels for your requirements and all their dependencies to a local directory:

$ pip install wheel
$ pip wheel --wheel-dir=/local/wheels -r requirements.txt

#And *then* to install those requirements just using your local directory of wheels (and not from PyPI):

$ pip install --no-index --find-links=/local/wheels -r requirements.txt
```

安装特定的源文件

```shell
$ pip install ./downloads/SomePackage-1.0.4.tar.gz
$ pip install http://my.package.repo/SomePackage-1.0.4.zip
```

安装git源

```shell
$ pip install -e git+https://git.repo/some_pkg.git#egg=SomePackage          # from git
$ pip install -e svn+svn://svn.repo/some_pkg/trunk/#egg=SomePackage         # from svn

$ pip install -e git+https://git.repo/some_pkg.git@feature#egg=SomePackage  
# from 'feature' branch

$ pip install -e "git+https://git.repo/some_repo.git#egg=subdir&subdirectory=subdir_path" # install a python package from a repo subdirectory
```

## pip列出已安装的包

```
$ pip list
docutils (0.9.1)
Jinja2 (2.6)
Pygments (1.5)
Sphinx (1.1.2)
```

## pip列出待更新的包

```
$ pip list --outdated
  SomePackage (Current: 1.0 Latest: 2.0)
```

## pip查看包信息

```
$ pip show --files SomePackage
  Name: SomePackage
  Version: 1.0
  Location: /my/env/lib/pythonx.x/site-packages
  Files:
   ../somepackage/__init__.py
   [...]
```

## pip升级包

```
$ pip install --upgrade SomePackage
  [...]
  Found existing installation: SomePackage 1.0
  Uninstalling SomePackage:
    Successfully uninstalled SomePackage
  Running setup.py install for SomePackage
  Successfully installed SomePackage
```

## pip卸载包

```
$ pip uninstall SomePackage
  Uninstalling SomePackage:
    /my/env/lib/pythonx.x/site-packages/somepackage
  Proceed (y/n)? y
  Successfully uninstalled SomePackage
```

## pip参数解释

**Usage**

```
pip <command> [options]
```

| Commands  | 说明                |
| --------- | ----------------- |
| install   | 安装                |
| download  | 从PyPI、VCS、本地..安装包 |
| uninstall | 卸载                |
| freeze    | 按着规定格式列出已安装包      |
| list      | 列出已安装包，包括可编辑的     |
| show      | 显示包详细信息           |
| search    | 搜索                |
| wheel     | 按照你的要求和依赖造轮子      |
| hash      | 计算本地包归档时的hash值    |



| General Options             | 说明                                                         |
| --------------------------- | ------------------------------------------------------------ |
| -h, --help                  | 显示帮助                                                     |
| -v, --verbose               | 详细信息                                                     |
| -V, --version               | 当前版本                                                     |
| -q, --quiet                 | 简略信息                                                     |
| --log `<path>`              | 添加详细信息的路径                                           |
| --proxy `<proxy>`           | 代理  [user:passwd@]proxy.server:port                        |
| --retries `<retries>`       | 重新连接（默认5次）                                          |
| --timeout `<sec>`           | 连接超时时间 (默认15秒)                                      |
| --exists-action `<action>`  | 当路径已存在时默认的操作: (s)witch, (i)gnore, (w)ipe, (b)ackup,(a)bort |
| --cert `<path>`             | 证书                                                         |
| --cache-dir `<dir>`         | 缓存路径                                                     |
| --no-cache-dir              | 取消缓存路径                                                 |
| --trusted-host `<hostname>` | 添加信任的网址                                               |

## 国内源

阿里云 [http://mirrors.aliyun.com/pypi/simple/](http://mirrors.aliyun.com/pypi/simple/)

中国科技大学 [https://pypi.mirrors.ustc.edu.cn/simple/ ](https://pypi.mirrors.ustc.edu.cn/simple/%20)

豆瓣(douban) [http://pypi.douban.com/simple/](http://pypi.douban.com/simple/) 

清华大学 [https://pypi.tuna.tsinghua.edu.cn/simple/](https://pypi.tuna.tsinghua.edu.cn/simple/)

中国科学技术大学 [http://pypi.mirrors.ustc.edu.cn/simple/](http://pypi.mirrors.ustc.edu.cn/simple/)

例：sudo easy_install -i [http://pypi.douban.com/simple/](https://pypi.douban.com/simple/) saltTesting