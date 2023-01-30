# JMeter菜单栏-运行&选项

## 本章要点
1. 运行模块介绍
2. 选项模块介绍


## 运行模块

本篇文章介绍运行下拉菜单，先不介绍远程相关的知识。在后续使用到时再详细介绍。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230128152343.png)

### 启动

启动运行当前的测试计划。

### 不停顿开始

`Start no pauses`：脚本无停顿启动运行测试计划。

#### 注意

1. 可以忽略脚本的定时器 

2. 再启动时运行更快

### 清除

清除选中监听器的执行结果。

>一个测试脚本内有多个监听器，比如：查看结果树、聚合报告。

>选中**查看结果树**点击**清除**，只清除结果树的运行结果不清除聚合报告的数据。

#### 清除全部
清除所有监听器的执行结果。

>无论选中哪个监听器，对应当前测试计划下的所有结果都被清除。

## 选项模块

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230128171027.png)


### 选择语言

最常用的就是语言的切换，根据自己习惯切换到常用语言。

#### 问题

每次打开界面都需要进行选择语言，不会在`JMeter`退出界面后进行保存。

#### 解决方案

如果想要解决该问题，可以直接修改配置文件`{jmeter_path}/bin/jmeter.properties `。
```
#Preferred GUI language. Comment out to use the JVM default locale's language.
#language=en
language=zh_CN
```


### 日志查看
选择日志查看，可以看到在右下方有对应的日志框显示。


![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230128173324.png)

### 全部折叠

- `Collapse All`:测试计划下的所有组件都折叠起来。


### 全部展开
- `Expand All`：只要是折叠的组件全部打开。


## 总结
- 运行下拉菜单中点击**不停顿开始**节省脚本测试时间。
- 选项下拉菜单中可以直接把所有组件进行折叠或者展开。


