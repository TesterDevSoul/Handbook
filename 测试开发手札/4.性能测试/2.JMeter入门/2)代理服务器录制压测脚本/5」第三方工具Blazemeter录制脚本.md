# 第三方工具Blazemeter录制脚本
## 本章要点
1. 要点一
1. 要点
1. 要点
1. 要点

## BlazeMeter安装和注册

首先来看一下对应的`BlazeMeter`官方对于[Chrome扩展的帮助文档](https://guide.blazemeter.com/hc/en-us/articles/206732579-Chrome-Extension)。可以看到在帮助文档页面，不只有对应如何结合`JMeter`进行性能测试还有`Blazemeter`对应的`API`文档。


`BlazeMeter`是一款与`Apache JMeter`兼容的`chrome`插件，采用`BlazeMeter`可以方便的进行流量录制和脚本生成，作为接口测试脚本编写的一个基础。

首先录制出需要的接口信息，再基于录制后的脚本进行优化来提高接口自动化的效率。记录所有浏览活动以创建`JMeter`脚本，并自动将其上传到`BlazeMeter`平台。



### 安装BlazeMeter

`Blazemeter`是一个测试平台，可以直接在`Chrome`浏览器中通过[扩展程序](https://chrome.google.com/webstore/detail/blazemeter-the-continuous/mbopgmdnpcbohhpnfglgohlbhfongabi?hl=zh-CN)进行安装，如果大家不能打开网站可以直接安装扩展程序[Blazemeter](Blazemeter-crx/mbopgmdnpcbohhpnfglgohlbhfongabi_v5.2.0.crx)。

点击Chrome浏览器右上角图标，选择  **更多工具**——>**扩展程序**，将`blazeMeter_v5.2.0.crx`文件直接拖拽进入扩展程序空白处，`BlazeMeter`插件自动安装，出现红框部分表示插件安装成功：

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230207153832.png)

注意⚠️：

- `Chrome`浏览器版本为**58**以上版本。
- `BlazeMeter`版本：5.5.0






点击浏览器对应`BlazeMeter`图标可以看到录制面板。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230207154808.png)


点击右上角的登录等待几分钟，进入到登录/注册页面，如果没有账号则根据页面相关信息

在


![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230207175339.png)





登录注册

，等待几分钟左右进入注册界面，根据相关提示填入用户名和邮箱信息，保存即可进入BlazeMeter界面。此时，再进入插件界面用户已自动登录http://，参见图1-3。



## 总结
- 总结一
- 总结二
- 总结三


[项目演示地址](https://github.com/testeru-pro/junit5-demo/tree/main/junit5-basic)
