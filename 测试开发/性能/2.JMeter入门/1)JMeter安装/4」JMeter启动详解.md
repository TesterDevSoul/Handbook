# JMeter启动详解
## 本章要点
1. 要点一
1. 要点
1. 要点
1. 要点

## 正文
## JMeter启动日志

`Java`版本为**8**的`JMeter`启动日志：
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116145155.png)

`Java`版本为**11**的`JMeter`启动日志：

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116145606.png)


##### WARNING
```bash
WARNING: package sun.awt.X11 not in java.desktop
```
该警告不需要管，如果想要进行修复，则使用Java8的版本即可修复。
##### 提示
```bash
# 不要使用GUI模式进行负载测试 GUI模式只是压测脚本的创建和调试
Dont use GUI mode for load testing !, only for Test creation and Test debugging.
# 如果想要进行负载测试 使用CLI模式 即非GUI模式 -- 静默压测会详细介绍
For load testing, use CLI Mode (was NON GUI):
   jmeter -n -t [jmx file] -l [results file] -e -o [Path to web report folder]
# 可以增加Java的堆来满足压测需求
& increase Java Heap to meet your test requirements:
# 修改JMeter文件的Java堆变量
   Modify current env variable HEAP="-Xms1g -Xmx1g -XX:MaxMetaspaceSize=256m" in the jmeter batch file
```



##### 报错：_TIPropertyValueIsValid called with 4 on nil context!

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116143106.png)

如果遇到该报错，可以参考该[issue](https://github.com/apache/jmeter/issues/5533)的解决方案。



**解决方案**：**修改对应`Java`版本号**或者**重新命令行启动**`JMeter`即可解决。


## JMeter界面
`JMeter`的主界面主要分为**菜单栏**、**工具栏**、**树状组件栏**和**组件内容栏**。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116150926.png)

### 菜单栏

全部的功能的都包含在菜单栏中。

### 工具栏

工具栏中的按钮在菜单栏内都可以找到，工具栏就相当于菜单栏常用功能的快捷按钮。

### 树状组件栏

树状组件栏通常用来显示 **测试用例**（计划）及其子组件。

### 组件内容栏

配合树状组件栏，树状组件栏中点击哪个组件，组件内容栏中就显示该组件的内容和配置。


## 模块



### 1. 文件

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116154447.png)


###### 打开
打开一个`JMX`文件。

###### 模板...
对常用的功能使用指导。主要有**录制**、**JDBC测试**、**BeanShell使用**、**构建Web测试计划**
等等，分为**基本步骤**和**详细截图**。 如果点用户链接，则会链接到`Apache JMeter` 官网查看详细的步骤和截图。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116155839.png)

>选择`构建web测试计划`后点击`create`则会直接在`GUI`界面创建整体模版，如下：
    ![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116160553.png)

**那创建的这些模版的脚本在JMeter的哪个路径下存在呢？**

打开`JMeter`安装路径，可以看到在`{jmeter_path}/bin/templates`文件夹下有所有的模板选项下的脚本。


![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116161740.png)


###### 合并

将多个`JMX`合并为一个。

>把多个`JMX`文件打开放在同一个测试计划下，先打开的组件放在上面。
###### 保存
仅保存当前的测试计划。
###### 保存测试计划为
将测试计划另存为在硬盘的指定位置。


###### 选中部分保存为...
选中的组件，比如线程组，会直接保存为新的测试计划。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116174134.png)




另存为：可以对工作台和测试计划或者测试例另存为JMX 注意另存为是点哪个位置，存的就是哪个内容。
save as Test fragment：存为一个测试片段，只有线程组、测试计划、工作台不能 保存为一个测试片段。
Revert：还原，将现在的jmx还原为已经保存过的JMX


1. 编辑

Save Node As Image（保存节点为图片）: 将菜单的配置GUI保存为图片。
Save Screen As Image（保存屏幕为图片）： 将整个jmeter界面保存为图片。
Toggle（切换）：类似于java中设置断点的意思。
3. 查找

Search: 搜索所有配置中匹配的项，匹配成功显示为红色。
Reset Search： 重置搜索，清除搜索结果。
4. 运行

启动： 启动运行测试计划
Start no pauses（不停顿开始）: 无停顿启动运行测试计划 1，可以忽略定时器 2，再启动时运行更快
远程启动/停止： 指定一个远程agent运行/停止测试计划。
远程全部启动/停止: 让所有远程agent运行/停止测试。
停止： 停止执行测试计划。
关闭: 关闭测试计划。
Remote Shutdown： 关闭一个指定远程agent。
Remote Shutdown All: 关闭所有远程agent。
远程退出： 指定一个远程agent退出执行。
远程退出全部: 所有远程agent退出执行。
清除： 清除选择菜单的执行结果。
清除全部: 清除所有菜单的执行结果。
5. 选项

函数助手对话框： 在编写脚本的时候，使用函数助手可以协助生成指定的代码。
外观： jmeter界面样式。
Log Viewer： 日志查看器，选中后可以在右下方查看运行日志。
SSL管理器: 导入外置的SSL管理器，用于更好的管理证书, JMeter代理服务器不支持记录 SSL(https)。
选择语言： 选择界面的语言，目前支持中文、英文、法语、德语等等。中文版很多翻译不全，可以直接使用英文版的。
Collapse All: 展开所有菜单。
Expand All： 折叠所有菜单
6. 帮助

What’s this node?： 当鼠标放在某个菜单的时候显示其含义。
Enable debug： 开启调试。
Disable debug: 取消调试。
Create a heap dump： 创建堆转储。这是创建当JVM崩溃的堆转储。这个文件可以用堆分析工具（如JHAT），以确定根本原因进行分析。


## 总结
- 总结一
- 总结二
- 总结三


[项目演示地址](https://github.com/testeru-pro/junit5-demo/tree/main/junit5-basic)
