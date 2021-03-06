---
title: Python命名规范
date: 2017/10/17 20:45:32
tags: 
- dev
- Python
categories:
- [开发,Py系列]
---
**Tips：**
> module_name
>
> package_name
>
> ClassName
>
> method_name
>
> ExceptionName
>
> function_name
>
> GLOBAL_VAR_NAME
>
> instance_var_name
>
> function_parameter_name
>
> local_var_name	

<!--more-->

## 应该避免的名称

    1. 单字符名称, 除了计数器和迭代器.
    2. 包/模块名中的连字符(-)
    3. 双下划线开头并结尾的名称(Python保留, 例如__init__)

## 命名约定

    1. 所谓”内部(Internal)”表示仅模块内可用, 或者, 在类内是保护或私有的.
    2. 用单下划线(_)开头表示模块变量或函数是protected的(使用import * from时不会包含).
    3. 用双下划线(__)开头的实例变量或方法表示类内私有.
    4. 将相关的类和顶级函数放在同一个模块里. 不像Java, 没必要限制一个类一个模块.
    5. 对类名使用大写字母开头的单词(如CapWords, 即Pascal风格), 但是模块名应该用小写加下划线的方式(如lower_with_under.py). 尽管已经有很多现存的模块使用类似于CapWords.py这样的命名, 但现在已经不鼓励这样做, 因为如果模块名碰巧和类名一致, 这会让人困扰.

## Python之父Guido推荐的规范

| Type                                   | Public             | Internal                                 |
| -------------------------------------- | ------------------ | ---------------------------------------- |
| Modules(模块)                            | lower_with_under   | _lower_with_under                        |
| Packages(包)                            | lower_with_under   |                                          |
| Classes(类)                             | CapWords           | _CapWords                                |
| Exceptions(异常)                         | CapWords           |                                          |
| Functions(函数)                          | lower_with_under() | _lower_with_under()                      |
| Global/Class(全局/类)  Constants(常量)      | CAPS_WITH_UNDER    | _CAPS_WITH_UNDER                         |
| Global/Class        Variables(变量)      | lower_with_under   | _lower_with_under                        |
| Instance Variables             (实例化对象) | lower_with_under   | _lower_with_under (protected) or __lower_with_under (private) |
| Method Names(方法名)                      | lower_with_under() | _lower_with_under() (protected) or __lower_with_under() (private) |
| Function/Method Parameters(参数)         | lower_with_under   |                                          |
| Local Variables(局部变量)                  | lower_with_under   |                                          |
