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
1. 压测脚本创建
2. GUI界面运行脚本
3. 使用监听器查看结果（树或表中的结果）
4. 将 `jmx` 文件运行到非 `GUI` 模式并生成 `HTML` 报告

#### 前置条件

1. `Java`环境安装配置成功。
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
##### 3)HTTP请求编写 
接下来搜索可在 Internet 上免费获得的REST API 。我们将以 Reqres API 为例。
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230107100649.png)

GET请求如下：
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230107100755.png)
现在你有了API，从链接中找出服务器名称、路径和参数。在JMeter 测试计划的HTTP 请求中复制这些值。
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230107100941.png)

##### 4）查看测试结果
添加一些监听器（简单的**数据写入器**）并将结果存储在csv文件中


对于添加侦听器，导航到 线程组(Thread Group) -> 添加(Add) -> 侦听器（简单数据编写器）

### 生成报告的两种方式：
a) 使用 GUI 模式：首先，在任意位置创建一个文件夹

在 JMeter 中转到工具 -> 生成 HTML 报告
## 总结
- Selenium Grid 概念
- Selenium Grid 使用场



http://www.ishatrainingsolutions.org/2020/06/30/jmeter-html-dashboard-report-generation/