# JMeter界面模块-编辑&查找
## 本章要点
1. 编辑模块功能介绍：截图
1. 查找模块功能介绍

## 编辑模块

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230128144912.png)

[示例脚本地址](GUI线程组截屏.jmx)

### 合并
选中测试计划组件后，选择编辑下拉的合并和文件模块的合并功能一致。

### 保存节点为图片

`Save Node As Image`：将选中组件的具体配置`GUI`界面保存为图片，**不显示**左侧树状组件栏。

保存的图片以`png`结尾，图片名默认为组件名称。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230128145612.png)


![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/HTTP.png)

### 保存屏幕为图片

`Save Screen As Image`：将整个`JMeter`界面保存为图片，**显示**左侧树状组件栏。

保存的图片以`png`结尾，图片名默认为当前选中的组件名称。

##### 线程组

保存线程组图片如下：

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/GUI.png)

##### HTTP请求

保存`HTTP`请求组件图片如下：

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/HTTP1.png)


### 切换

`Toggle`：将启用变为禁用，禁用变为启用。更改组件现有状态。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230128151548.png)

点击切换后，当前组件的状态进行更改。
>类似于java中设置断点的意思;网上博客的内容，不准确。


#### 切换与禁用区别


- 启用/禁用：选择启用或禁用其执行相应。

- 切换：将启用变为禁用，禁用变为启用。

### 保存为测试片段

选中测试计划下的组件，选择编辑，下拉列表有**保存为测试片段**，该选项与文件模块的**保存为测试片段**功能一致。


## 查找模块

### 查找

`Search`: 搜索所有配置中匹配的项，匹配成功显示为**红色**，匹配组件的上层级组件显示为蓝色。


![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230128151815.png)


#### 注意⚠️

- 查找无论当前组件是否被禁用，都可以被查找到。


- 如果需要正则匹配，则勾选☑️上正则表达式选项，即可填写正则表达式。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230128162156.png)

- 查找可以是对应组件内的域名，也可以是具体的某个参数值，都可以搜索到。


### 重置搜索

`Reset Search`：清除搜索结果，对应匹配的红色框及上一层级的蓝色框消失。



## 总结

- 截图当前界面可以使用编辑下的`保存**为图片`，若想要**组件树**则选择**屏幕**，若只是想要当前组件的详细配置则选择**节点**。
- 查找可以使用正则匹配，会匹配出所有包含的节点。