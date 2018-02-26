---
title: Jmeter学习笔记
date: 2017/10/17 19:59:39
tags:
- test
categories:
- [软件测试, 性能测试]
---
## Aggregate Report

> For each request, it totals the response information and provides request count, min, max, average, error rate, approximate throughput (request/second) and Kilobytes per second throughput.	

对于每个请求，它总计响应信息，并提供请求计数，最小值，最大值，平均值，错误率，近似吞吐量（请求/秒）和每秒千字节吞吐量。

<!--more-->

| 列标题             | 含义             |
| --------------- | -------------- |
| Label           | 样品的标签          |
| \# Samples      | 具有相同标签的样本数     |
| Average         | 一组结果的平均时间      |
| Median          | 一组结果中间的时间      |
| 90% Line        | 90％的样品不超过这个时间  |
| 95% Line        | 95％的样品不超过这个时间  |
| 99% Line        | 99％的样品不超过这个时间  |
| Min             | 具有相同标签的样品的最短时间 |
| Max             | 具有相同标签的样品的最长时间 |
| Error %         | 错误请求的百分比       |
| Throughput      | 吞吐量(每秒、分、时请求数) |
| Received KB/sec | 每秒接收字节数        |
| Sent KB/sec     | 每秒传输字节数        |

## 元件的执行顺序

测试计划中的元件按照如下顺序执行。

1. 配置元件（config elements ）
2. 前置处理程序（Per-processors）
3. 定时器（timers ）
4. 取样器（Sampler）
5. 后置处理程序（Post-processors） （除非Sampler 得到的返回结果为空）。
6. 断言（Assertions）（除非Sampler 得到的返回结果为空）。
7. 监听器（Listeners）（除非Sampler 得到的返回结果为空）。

## 常见接口测试工具

* 典型商业工具： loadrunner,soapui
* 典型开源工具: jmeter jsoup httpclient python中的urllib2,urllib库
* 扩展插件： Poster、 POSTMAN

## 接口测试与抓包

* 协议原理
* 协议捕获（Firebug、 fiddler、 Httpwatch）
* 协议变更 (Poster、 PostMan、 HttpRequest、 Temper Data）
* http抓包： HTTP Analyzer
* 通用数据抓包： MiniSniffer
* 进程级抓包： WSExplorer 

## Bean Shell常用内置变量

JMeter在它的BeanShell中内置了变量，用户可以通过这些变量与JMeter进行交互，其中主要的变量及其使用方法如下:

- **log**：写入信息到jmeber.log文件，使用方法：```log.info(“This is log info!”);```
- **ctx**：该变量引用了当前线程的上下文，使用方法可参考：[org.apache.jmeter.threads.JMeterContext](http://jmeter.apache.org/api/org/apache/jmeter/threads/JMeterContext.html)。
- **vars** - (JMeterVariables)：操作jmeter变量，这个变量实际引用了JMeter线程中的局部变量容器（本质上是Map），它是测试用例与BeanShell交互的桥梁，常用方法：
  - ```vars.get(String key)```：从jmeter中获得变量值
  - ```vars.put(String key，String value)```：数据存到jmeter变量中

更多方法可参考：[org.apache.jmeter.threads.JMeterVariables](http://jmeter.apache.org/api/org/apache/jmeter/threads/JMeterVariables.html)

- **props** - (JMeterProperties - class java.util.Properties)：操作jmeter属性，该变量引用了JMeter的配置信息，可以获取Jmeter的属性，它的使用方法与vars类似，但是只能put进去String类型的值，而不能是一个对象。对应于java.util.Properties。 
  - ```props.get("START.HMS");```注：START.HMS为属性名，在文件jmeter.properties中定
  - ```props.put("PROP1","1234"); ```


- **prev** - (SampleResult)：获取前面的sample返回的信息，常用方法：
  - getResponseDataAsString()：获取响应信息
  - getResponseCode() ：获取响应code

更多方法可参考：[org.apache.jmeter.samplers.SampleResult](http://jmeter.apache.org/api/org/apache/jmeter/samplers/SampleResult.html)

- sampler - (Sampler)：gives access to the current sampler

## 性能测试类型

1. 基准测试：在给系统施加较低压力时，查看系统的运行状况并记录相关数做为基础参考
2. 负载测试：是指对系统不断地增加压力或增加一定压力下的持续时间，直到系统的某项或多项性能指标达到安全临界值，例如某种资源已经达到饱和状态等 。
3. 压力测试：压力测试是评估系统处于或超过预期负载时系统的运行情况，关注点在于系统在峰值负载或超出最大载荷情况下的处理能力。
4. 稳定性测试：在给系统加载一定业务压力的情况下，使系统运行一段时间，以此检测系统是否稳定。
5. 并发测试：测试多个用户同时访问同一个应用、同一个模块或者数据记录时是否存在死锁或者其他性能问题。

