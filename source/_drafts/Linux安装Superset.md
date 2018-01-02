---
title: Linux安装Superset
date: 2017/10/17 20:53:04
tags:
- Linux
---
# linux系统下安装Superset

## 1.安装依赖

```shell
$  yum upgrade python-setuptools
$  yum install gcc gcc-c++ libffi-devel python-devel python-pip python-wheel openssl-devel libsasl2-devel openldap-devel sqlite-devel
$  pip install --upgrade setuptools pip
```

<!--more-->

## 2.安装superset

```shell
# Install superset
$ pip install superset

# 建议使用国内源
$ pip install superset -i http://pypi.douban.com/simple --trusted-host=pypi.douban.com

# 如果安装报错，根据报错的内容补全依赖，例：
g++: error trying to exec 'cc1plus': execvp: 没有那个文件或目录
$ yum install gcc-c++

# 若有包源丢失，例如numpy包缺少，可手动安装
$ pip install numpy -i http://pypi.douban.com/simple --trusted-host=pypi.douban.com

# Create an admin user (you will be prompted to set username, first and last name before setting a password)
$ fabmanager create-admin --app superset

# Initialize the database
$ superset db upgrade

# Load some data to play with
$ superset load_examples

# Create default roles and permissions
$ superset init

# Start the web server on port 8088, use -p to bind to another port
$ superset runserver
# 推荐使用nohup
$ nohup superset runserver -p 8088 &
```

## 3.登录

浏览器输入`localhost:8088`

## 4.说明

配置文档位置`$PYTHONPATH/superset/config.py`



官方文档：[http://airbnb.io/superset/installation.html](http://airbnb.io/superset/installation.html)

开源地址：[https://github.com/airbnb/superset](https://github.com/airbnb/superset)

## 5.链接数据库

Here’s a list of some of the recommended packages.[SqlAlchemy docs](http://docs.sqlalchemy.org/en/rel_1_0/core/engines.html#database-urls)

| database   | pypi package                            | SQLAlchemy URI prefix       |
| ---------- | --------------------------------------- | --------------------------- |
| MySQL      | `pip install mysqlclient`               | `mysql://`                  |
| Postgres   | `pip install psycopg2`                  | `postgresql+psycopg2://`    |
| Presto     | `pip install pyhive`                    | `presto://`                 |
| Oracle     | `pip install cx_Oracle`                 | `oracle://`                 |
| sqlite     |                                         | `sqlite://`                 |
| Redshift   | `pip install sqlalchemy-redshift`       | `postgresql+psycopg2://`    |
| MSSQL      | `pip install pymssql`                   | `mssql://`                  |
| Impala     | `pip install impyla`                    | `impala://`                 |
| SparkSQL   | `pip install pyhive`                    | `jdbc+hive://`              |
| Greenplum  | `pip install psycopg2`                  | `postgresql+psycopg2://`    |
| Athena     | `pip install "PyAthenaJDBC>1.0.9"`      | `awsathena+jdbc://`         |
| Vertica    | `pip install sqlalchemy-vertica-python` | `vertica+vertica_python://` |
| ClickHouse | `pip install sqlalchemy-clickhouse`     | `clickhouse://`             |

## 6.修改表单

On the resulting page, click on the **List Table Column** tab. Here, you’ll define the way you can use specific columns of your table when exploring your data. We’ll run through these options to describe their purpose:

- If you want users to group metrics by a specific field, mark it as **Groupable**.
- If you need to filter on a specific field, mark it as **Filterable**.
- Is this field something you’d like to get the distinct count of? Check the **Count Distinct** box.
- Is this a metric you want to sum, or get basic summary statistics for? The **Sum**, **Min**, and **Max**columns will help.
- The **is temporal** field should be checked for any date or time fields. We’ll cover how this manifests itself in analyses in a moment.

## 7.Unicode

```
"mysql+pymysql://scott:tiger@localhost/test?charset=utf8"
```