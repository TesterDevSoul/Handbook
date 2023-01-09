# 静默压测生成HTML报告

## 课程目标
1.  Selenium Grid 概述
2.  Selenium Grid 使用场景
3.  Selenium Grid 运行机制
4.  Selenium Grid 执行流程


## 静默压测生成HTML报告
查看[官网](https://jmeter.apache.org/usermanual/generating-dashboard.html)，对应的显示一个HTML的文件报告，但是在这个页面并没有告诉我们应该怎样去生成这样的报告，下面主要就给大家讲解一下对应的如何自动生成HTML报告并且可以自动的多并发执行。

### 静默压测生成HTML报告步骤
首先，我们先看一下对应生成HTML报告的步骤，依据以下步骤来生成：
1. 压测脚本创建 - 使用监听器查看结果（树或表中的结果）
2. GUI界面运行脚本
3. 将 `jmx` 文件运行到非 `GUI` 模式并生成 `HTML` 报告

#### 前置条件

1. `Java`环境安装配置成功。Java 8+，建议jdk11。
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230106140728.png)

1. `Apache JMeter`下载安装成功。
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230106140822.png)


如果满足以上条件，就可以进行对应的压测脚本的创建及运行。
#### 1. 压测脚本创建
安装`JMeter`，以`GUI`模式启动`JMeter`并构建测试计划。

如果配置了全局环境变量则直接命令行输入`jmeter`启动`JMeter`的界面；

如果没有配置全局变量则命令行`cd`到`{jmeter_path}/bin`路径下，再输入`jmeter`以启动`JMeter`的界面。
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230106115317.png)

##### 1）打开JMeter并添加线程组
要添加线程组，测试计划(Test Plan) -> 添加(Add) -> 线程(Threads) -> 线程组(Thread Group)
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230107092806.png)

##### 2）添加HTTP请求
导航到 线程组(Thread Group) -> 添加(Add) -> 采样器(Sampler) -> HTTP 请求(HTTP Request)
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230107094231.png)
##### 3）HTTP请求编写 
接下来搜索可在 Internet 上免费获得的REST API 。我们将以 Reqres API 为例。
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230107100649.png)

GET请求如下：
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230107100755.png)
现在你有了API，从链接中找出**服务器名称**、**路径**和**参数**。在JMeter 测试计划的 HTTP 请求中复制这些值。
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230107100941.png)

##### 4）查看测试结果
添加一个监听器（简单的**数据写入器**）并将结果存储在csv文件中。
对于添加侦听器，导航到 测试计划(Test Plan) -> 添加(Add) -> 侦听器(Listener)  -> 查看结果树(View Results Tree)


![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230107101442.png)



每个监听器中，都会有一个**所有数据写入一个文件**的功能。在创建查看结果树时需要对写出的文件地址进行配置，选择本地任意一个位置后面跟上数据输出的文件名。

我们可以从弹窗的文件类型中看到，支持的文件类型有三种：`XML`、`jtl`、`CSV`。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230108121815.png)

哪种类型是JMeter默认的呢？
打开`{jmeter_path}/bin/jmeter.properties`文件，可以看到`output_format`的参数值默认为`csv`，所以`CSV`是JMeter的默认类型。
```
#jmeter.save.saveservice.output_format=csv
```
当我们选择一个路径时，可以选择**已存在的文件**，也可以选择**未存在的文件**。文件名可以以`.csv`或`.jtl`结尾，本文使用`.jtl`结尾文件。

注意⚠️：建议使用**未存在**文件。
>JMeter默认参数配置中，`resultcollector.action_if_file_exists=ASK`，默认是询问用户。还有`APPEND`，`DELETE`选择使用。
```
# Used to control what happens when you start a test and
# have listeners that could overwrite existing result files
# Possible values:
# ASK : Ask user 询问用户
# APPEND : Append results to existing file 在已经存在文件后追加结果
# DELETE : Delete existing file and start a new file  删除已经存在的文件并创建一个新的
#resultcollector.action_if_file_exists=ASK
```
>若文件为已存在的，则在运行时会弹窗提示，弹窗提示如下图：


![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230108121415.png)



注意⚠️：一般请求的参数化使用的是`csv`文件，压测结果存储为`jtl`文件，进行区分，不建议使用`xml`存储结果。
>因为XML结果文件不能像csv、jtl一样直接命令行生成HTML报告，如果生成还需要与ant集成。

#### 2. GUI界面运行脚本
##### 5）运行
保存测试 (`.jmx`) 并运行它。只需单击**绿色按钮**或快捷键{**Window**}`Ctrl+R`/{**Mac**}`Command+R`即可运行测试。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230107101938.png)
上面的测试结果显示了HTTP 请求服务器的请求和响应。


##### jtl 文件查看
默认配置下，jtl文件保存的字段为：
```
timeStamp,elapsed,label,responseCode,responseMessage,threadName,dataType,success,failureMessage,bytes,sentBytes,grpThreads,allThreads,URL,Latency,IdleTime,Connect
1673149864221,6824,GET API,200,OK,Thread Group 1-1,text,true,,1744,123,1,1,https://reqres.in/api/users?page=2,6823,0,1
```
|字段|说明|
|---|---|
|timeStamp|时间戳，毫秒；如：1673149864221|
|elapsed|耗时，毫秒；从发送请求到收到最后一个响应，所花费的时间；不包括渲染请求所花费的时间，同时也不包括处理客户端脚本所花费的时间|
|label|取样器名称 如：GET API|
|responseCode|HTTP响应code码；如：200|
|responseMessage|响应的message消息；如：OK|
|threadName|线程名；如：Thread Group 1-1|
|dataType|参数的数据类型；|
|success|请求是否成功；|
|failureMessage|响应的失败的message消息；|
|bytes|请求样本字节数|
|sentBytes|发送样本字节数|
|grpThreads|当前线程组的线程数|
|allThreads|所有线程组的线程数|
|URL|请求地址路径|
|Latency|延迟的耗时|
|IdleTime|空闲时间，毫秒；|
|Connect|连接建立的时间|


在这里，对应的请求和响应的body参数没有写入文件，因为jtl文件中这些参数主要是为了做性能分析生成图表进行使用。
#### 3. 生成报告

### 生成报告的两种方式
#### 1) 使用 GUI 模式生成报告

- 也就是需要**从独立的 csv/jtl 文件创建报告**。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230108150435.png)
###### 报错
```
Generating report
File '/**/api.jtl' does not contain the field names header, ensure the jmeter.save.saveservice.* properties are the same as when the CSV file was created or the file may be read incorrectly when generating report
An error occurred: null
```

- 由于没有头信息导致，需要添加上以下对应头信息：
```
timeStamp,elapsed,label,responseCode,responseMessage,threadName,dataType,success,failureMessage,bytes,sentBytes,grpThreads,allThreads,URL,Latency,IdleTime,Connect
```


首先，在任意位置创建一个文件夹

在 JMeter 中转到工具 -> 生成 HTML 报告


首先在结果文件上放置存储结果的 CSV 文件路径
在 User.properties 文件部分提到了 user.properties 文件的位置
在输出中，directory 放置新创建的文件夹路径


**在测试结束时创建报告**


## 总结
- Selenium Grid 概念




http://www.ishatrainingsolutions.org/2020/06/30/jmeter-html-dashboard-report-generation/