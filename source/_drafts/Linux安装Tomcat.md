---
title: Linux安装Tomcat
date: 2017/10/17 20:58:42
tags:
- Linux
categories:
- [运维, 环境]
---
## 解压缩

```shell
# mkdir /usr/local/tomcat

# cd /usr/local/tomcat

# tar -zxvf /software/apache-tomcat-7.0.54.tar.gz
```

<!--more-->

生成链接以便版本升级

```shell
# ln -s apache-tomcat-7.0.54 server
```

启动Tomcat

```shell
#cd /usr/local/tomcat/server/bin

#./startup.sh

Using CATALINA_BASE: /usr/local/tomcat/server

Using CATALINA_HOME: /usr/local/tomcat/server

Using CATALINA_TEMDIR: /usr/local/tomcat/server/temp

Using JRE_HOME: /usr/java/default

Using CLASS_PATH: /usr/local/tomcat/server/bin/bootstrap.jar:/usr/local/tomcat/server/bin/tomcat-juli.jar

Tomcat started.
```

测试Tomcat:
打开防火墙,使外部能访问

```shell
# /sbin/iptables -I INPUT -p tcp --dport 8080 -j ACCEPT

# service iptables save

# service iptables restart
```

或直接修改文件/etc/sysconfig/iptables.

```shell
# vi /etc/sysconfig/iptables

-A INPUT -p tcp -m tcp --dport 8080 -j ACCEPT

# service iptables restart
```

在浏览器输入: http://192.168.16.133:8080
如在本机可以输入: http://localhost:8080
出现tomcat的页面表示安装成功.

停止Tomcat
```shell
# shell./shutdown.sh
```

## 配置web管理帐号
   修改文件conf/tomcat-users.xml，在`<tomcat-users>`元素中添加帐号密码，需要指定角色.

```shell
# vi /usr/local/tomcat/server/conf/tomcat-users.xml
```

```xml
<tomcat-users>
    <user name="admin" password="admin" roles="admin-gui,manager-gui" />
</tomcat-users>
```


## 配置web访问端口
   可以修改conf目录下的文件server.xml，修改Connector元素(Tomcat的默认端口是8080)，需要重新启动Tomcat服务生效.

```shell
vi /usr/local/tomcat/server/conf/server.xml
```

```shell
<Connector port="80" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" /> 
```

## 配置https安全连接(ssl加密连接)
https连接需要用到数字证书与数字签名(MD5算法)
网站https连接首先需要申请数字证书，配置加密连接器，浏览器安装证书.
使用java的工具keytool产生数字证书

```shell
# keytool -genkey -alias tomcat -keyalg RSA
```

生成文件.keystore
注意:CN为主机名称，本机可用localhost
将文件.keystore放到Tomcat服务器的conf目录下

```shell
# cp .keystore /usr/local/tomcat/server/conf/
```

修改conf/server.xml文件，修改加密连接器，添加keystoreFile与keystorePass

```xml
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true"

            maxThreads="150" scheme="https" secure="true"

            clientAuth="false" sslProtocol="TLS" 

            keystoreFile="conf/.keystore" keystorePass="123456"/>
```

重新启动tomcat.浏览器输入https://localhost:8443访问,并安装证书.


## Tomcat的目录结构
| 目录       | 使用                                |
| -------- | --------------------------------- |
| ·bin     | 存放Tomcat的命令脚本文件                   |
| ·conf    | 存放Tomcat服务器的各种配置文件,最主要是server.xml |
| ·lib     | 存放Tomcat服务器支撑jar包                 |
| ·logs    | 存放日志文件                            |
| ·temp    | 存放临时文件                            |
| ·webapps | web应用所在目录，外界访问web资源的存放目录          |
| ·work    | Tomcat的工作目录                       |


## web应用的目录结构
webapp                                  -- web应用所在目录
|--- html, jsp, css, js文件等  -- 这些文件一般在web应用根目录下，根目录下的文件外界可以直接访问.
|--- WEB-INF 目录                 -- java类、jar包、web配置文件存在这个目录下，外界无法直接访问，由web服务器负责调用.
|--- classes 目录            -- java类
|--- lib 目录                    -- java类运行所需要的jar包
|--- web.xml 文件         -- web应用的配置文件


## 虚拟主机的配置
指定虚拟主机名,修改conf/server.xml,添加<host>元素.

```xml
<host name="hostname.domainname" appBase="/webapps">
<Context path="/webapp" docBase="/webapps/webapp"/>
</host>
```

例:

```xml
<host name="www.163.com" appBase="/webapps">
</host>
<host name="mail.163.com" appBase="/mailapps">
</host>
```

须设置DNS解析(host文件或DNS系统).

## web应用和虚拟目录的映射.
可以修改xml配置文件的`<Context>`元素来设置web应用和虚拟目录的映射.

| xml配置文件                                  | 设置web应用和虚拟目录的映射                          |
| ---------------------------------------- | ---------------------------------------- |
| ·conf/server.xml                         | 在<host>元素下添加`<Context path="/webdir" docBase="/webappdir"/>` |
| ·conf/context.xml                        | 添加<Context>元素所有web应用有效.            |
| ·conf/[enginename]/[hostname]/context.xml.default | [enginename]一般是Catalina，主机[hostname]的所有web应用有效. |
| ·conf/[enginename]/[hostname]/           | 在目录下任意建一个文件(扩展名xml),文件名即为虚拟目录名.多级目录使用#分割 |
| `.<Context docBase="/webappdir"/>`   | 缺省值web应用目录可以定义为ROOT.xml，添加`<Context docBase="/webappdir"/>`,需重新启动Tomcat服务器 |
| ·META-INF/context.xml                    | 可以将web应用放在webapps目录下让Tomcat服务器自动映射，适用开发环境，实际运用环境中不用自动映射 |

如没有修改配置文件，web应用目录为ROOT时则为默认web应用。


## web应用首页(welcome file)的配置
修改web应用的配置文件: [webapp]/WEB-INF/web.xml

```xml
<welcome-file-list>
  <welcome-file>index.html</welcome-file>
  <welcome-file>index.htm</welcome-file>
  <welcome-file>index.jsp</welcome-file>
</welcome-file-list>
```