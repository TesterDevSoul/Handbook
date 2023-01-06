# 静默压测生成HTML报告

## 课程目标
1.  Selenium Grid 概述
2.  Selenium Grid 使用场景
3.  Selenium Grid 运行机制
4.  Selenium Grid 执行流程


## 静默压测生成HTML报告步骤

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


## 总结
- Selenium Grid 概念
- Selenium Grid 使用场