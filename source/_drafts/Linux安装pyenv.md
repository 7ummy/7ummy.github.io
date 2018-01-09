---
title: Linux安装pyenv
date: 2017/10/17 20:13:55
tags:
- Linux
categories:
- [运维, 环境]
- [开发, Py系列, 环境]
---
## 1.安装python依赖

```shell
$ yum -y update
$ yum groupinstall -y development
$ yum install -y zlib-dev readline-devel openssl-devel sqlite-devel bzip2-devel 
```

<!--more-->

## 2.通过GIT安装(推荐)

```shell
$ curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash
```

## 3.修改配置文件

编辑配置文件`vi ~/.bash_profile`写入一下指令：

```shell
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

命令行使用source指令使配置生效`source ~/.bash_profile`

## 4.安装python

一般情况下`python install`指令下载缓慢，我们在*~/.pyenv*目录下创建一个*cache*文件夹存放python的tarball。

```shell
$ cd $HOME/.pyenv
$ mkdir cache
```

将tarball移动到*cache*目录下

```shell
$ mv Python-x.x.x.tar.xz $HOME/.pyenv/cache
```

然后再使用指令

```shell
$ pyenv install Python-x.x.x.tar.xz
```

注意使用`pyenv rehash`指令创建 shims

更新pyenv版本:`pyenv update`

---

## 卸载

Uninstall:

 `pyenv` is installed within `$PYENV_ROOT` (default: `~/.pyenv`). To uninstall, just remove it:

```shell
$ rm -fr ~/.pyenv
```

and remove these three lines from `.bashrc`:

```shell
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

If you need, export USE_GIT_URI to use git:// instead of https:// for git clone.

## 使用

**pyenv versions**

查看当前 pyenv 可检测到的所有版本，处于激活状态的版本前以 * 标示。

**pyenv install**

`pyenv install x.x.x`安装一个版本

**pyenv uninstall**

`pyenv uninstall x.x.x`卸载一个版本

**pyenv rehash**

为所有已安装的可执行文件 （如：`~/.pyenv/versions/*/bin/*`） 创建 shims，因此，每当你增删了 Python 版本或带有可执行文件的包（如 pip）以后，都应该执行一次本命令

**pyenv global**

设置面向程序的本地版本，通过将版本号写入当前目录下的 `.python-version` 文件的方式。通过这种方式设置的 Python 版本优先级较 global 高。pyenv 会从当前目录开始向上逐级查找 `.python-version` 文件，直到根目录为止。若找不到，就用 global 版本。

**pyenv shell**

设置面向 shell 的 Python 版本，通过设置当前 shell 的 `PYENV_VERSION` 环境变量的方式。这个版本的优先级比 local 和 global 都要高。`--unset` 参数可以用于取消当前 shell 设定的版本。

## Using pyenv virtualenv

```shell
$ pyenv virtualenv 3.6.1 venv36
```

### Create virtualenv from current version

```shell
$ pyenv version
3.6.1 (set by /home/yyuu/.pyenv/version)
$ pyenv virtualenv venv36
```

### 使用virtualenv

```shell
$ pyenv shell/global venv36
```

### Activate virtualenv

Some external tools (e.g. [jedi](https://github.com/davidhalter/jedi)) might require you to `activate` the virtualenv and `conda` environments.

If `eval "$(pyenv virtualenv-init -)"` is configured in your shell, `pyenv-virtualenv` will automatically activate/deactivate virtualenvs on entering/leaving directories which contain a `.python-version` file that lists a valid virtual environment. `.python-version` files denote local Python versions and can be created and deleted with the [`pyenv local`](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md#pyenv-local) command.

You can also activate and deactivate a pyenv virtualenv manually:

```
pyenv activate <name>
pyenv deactivate
```

### Delete existing virtualenv

Removing the directories in `$(pyenv root)/versions` and `$(pyenv root)/versions/{version}/envs` will delete the virtualenv, or you can run:

```
pyenv uninstall my-virtual-env
```