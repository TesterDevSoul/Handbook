# JMeter安装及配置-Mac
## 本章要点
1. 要点一
1. 要点
1. 要点
1. 要点

## 正文

在`Mac`上安装对应的`JMeter`工具有两种方式：一种直接借助**终端命令行**`brew`进行安装；另外一种和`Window`电脑一样去`JMeter`官网下载**压缩包安装**。



### 前置条件

1. `Java`环境安装配置成功。Java 8+，建议jdk11。
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230106140728.png)

1. `Apache JMeter`下载安装成功。
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230106140822.png)


```bash
bew install jmeter
```
默认安装的路径为`/usr/local/Cellar/jmeter/5.5`。

如果满足以上条件，就可以进行对应的压测脚本的创建及运行。
### 1. 压测脚本创建
安装`JMeter`，以`GUI`模式启动`JMeter`并构建测试计划。

如果配置了全局环境变量则直接命令行输入`jmeter`启动`JMeter`的界面；

如果没有配置全局变量则命令行`cd`到`{jmeter_path}/bin`路径下，再输入`jmeter`以启动`JMeter`的界面。
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230106115317.png)


##### 报错
配置完环境变量后，对应的命令行打开还是不能启动脚本，命令行提示：

```bash
jmeter: Permission denied【拒绝访问】
```

**解决方案**：给`jmeter`启动脚本增加权限。
```bash
chmod +x jmeter

# 移除对应的执行权限
chmod -x jmeter
```


>启动JMeter的界面化，其实就是启动的`{jmeter_path}/bin`下的`jmeter`脚本，Mac/Linux系统下是jmeter，Window系统下是jmeter.bat；<br>看一下脚本的内容：

- `#! /bin/sh`：说明是一个shell脚本。
- `JAVA_HOME`：电脑的环境变量需要配置该变量。
- `MINIMAL_VERSION=8`：启动JMeter的最低Java版本是8。
- `JAVA9_OPTS=`：JMeter也可以使用Java9,但是使用9的时候对应启动命令参数就有变化。
- `: "${HEAP:="-Xms1g -Xmx1g -XX:MaxMetaspaceSize=256m"}"`：JMeter使用的Java环境的基本堆大小。可以修改。
- `: "${JMETER_LANGUAGE:="-Duser.language=en -Duser.region=EN"}"`：默认的语言是英语，可以修改为中文。

## 总结
- 总结一
- 总结二
- 总结三


[项目演示地址](https://github.com/testeru-pro/junit5-demo/tree/main/junit5-basic)
