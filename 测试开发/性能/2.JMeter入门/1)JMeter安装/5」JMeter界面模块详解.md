# JMeter界面模块详解
## 本章要点
1. JMeter启动日志
1. JMeter界面介绍

## 模块详解
上面简单的介绍了一下对应的具体模块的功能说明，下面对具体的功能进行详细的使用说明。

### 1. 文件
首先来看第一个就是文件，在文件这个模块内有多个功能，分别是：新建、模版、打开、合并等等，下面根据常用的几个来进行功能的演示说明。


![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116154447.png)

#### 打开

打开一个当前硬盘上的压测脚本即`JMX`文件。

#### 模板...

**模板**是对常用的功能使用指导。

主要有**录制**、**JDBC测试**、**BeanShell使用**、**构建Web测试计划**
等等，每个功能都分为**基本步骤**和**详细截图**。

##### 步骤说明

在模板界面选择需要的模版后，点击`Useful links`「用户链接」，则会链接到`Apache JMeter` 官网查看该组件的详细步骤和截图。


![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116155839.png)

##### 模板构建脚本
###### 需求
下拉选择模板内的功能，构建一个web的测试计划模版脚本。

###### 步骤

1. 模板界面选择 **构建web测试计划** - `Building a Web Test Plan` 
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230128105709.png)


1. 点击`create`则会直接在`GUI`界面创建整体模版，如下：
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116160553.png)


###### 问

模版脚本都在`JMeter`哪里存在呢？

为什么在模版内选择对应功能就能创建出来相关脚本？

###### 答

打开`JMeter`安装路径，可以看到在`{jmeter_path}/bin/templates`文件夹下有所有的模板选项下的脚本。


![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116161740.png)

#### 合并

将多个`JMX`脚本文件合并为一个，也就是把多个`JMX`文件打开放在同一个测试计划下。

**注意⚠️**：先打开的脚本文件中测试计划下的组件会放在上面。
##### 需求

将**2**个脚本合并为一个脚本。

##### 准备

在这里准备了**2**个脚本，一个脚本为`ATest.jmx`，一个脚本为`BTest.jmx`。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230128111317.png)


##### 步骤

1. 打开新的测试计划，选择文件下的**合并**，根据路径选择`BTest.jmx`，可以看到当前脚本的测试计划下添加对应组件，但是该脚本还没有进行保存。

   ![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230128112255.png)

   ![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230128112821.png)

1. 再次选择合并，根据路径选择`ATest.jmx`，可以看到当前脚本的测试计划下继续添加`ATest`脚本的组件。

   ![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230128113051.png)


##### 注意

可以进行多个脚本的合并，没有个数限制。

合并选择对应文件后，组件会一直往后叠加。

##### 场景

功能点分开多个人编写压测脚本，最终链路压测或需求合并压测时，需要把多个压测脚本合并为一个脚本。

>使用文件的合并功能，可以节省



#### 保存

仅保存当前的测试计划。

#### 保存测试计划为

将测试计划另存为在硬盘的指定位置。

#### 选中部分保存为...

选中的组件，比如线程组，会直接保存为新的测试计划脚本。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116174134.png)




##### 保存为测试片段
存为一个测试片段，**线程组**、**测试计划**、**工作台**不能保存为一个测试片段。


如果选中则会提示如下报错：

```bash
One of the selected nodes cannot be put inside a Test Fragment
```

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/1674012683977.png)


###### 测试片段与线程组的区别

**测试片段**元素是一种特殊类型的控制器，它存在于测试计划树中，**与线程组元素处于同一级别**。

它与线程组的区别在于测试片段不会被执行，除非测试片段被**模块控制器**或`Include_Controller`引用。

**测试片段**纯粹用于测试计划中的**代码重用**。

###### 测试片段与线程组的区别

测试片段保存`HTTP`请求组件为新的`JMX`脚本文件。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230118115120.png)





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
