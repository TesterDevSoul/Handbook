# JMeter体系结构
## 本章要点
1. 要点一
1. 要点
1. 要点
1. 要点

## JMeter基本组件




### 八大组件

1. Sampler「**采样器/取样器**」
2. Logic Controller「**控制器**」
3. Config Elements「**配置元件**」
4. Timer「**定时器**」
5. Assertions「**断言**」
6. Listener「**监听器**」
7. Pre/Post-processors 「**前置/后置处理器**」
8. Thread Group「**线程组**」



#### 元件

元件代表JMeter工具菜单中一个子菜单/功能，比如：HTTP请求、JDBC 请求、事务控制器、响应断言等，就是一个元件。

>向百度服务器发送一个HTTP协议的GET请求，这个请求是由一个HTTP请求取样器来完成，这个HTTP请求取样器就是元件。

**在树状组件栏中添加进来的都是元件**。


#### 组件

一组元件的集合（一个/多个），比如逻辑控制器中有事务控制器、仅一次控制器、循环控制器等，这些都是元件。但是它们被归类到逻辑控制器中，**逻辑控制器**就是组件。


#### 元件VS组件

- 多个元件叫组件。

- 元件是JMeter中最小的添加的内容。

- 组件是一个元件的集合。



**不同的元件作用范围不同。**
>`Header Manager`可以影响全局所有的`Http Sampler`，也可以只影响某一个`Http Sampler`，看`Header Manager`所处位置的作用范围而决定。

**不同元件对应执行时序点也不同。**

>断言组件Assertions中查看结果树元件，就是为了校验请求是否通过。所以，Assertions元件一定是运行在Sample之后，如果上来就先运行断言组件对应的压测脚本是没有任何意义的。   




### 组件结构图

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230216140127.png)

取样器、断言、监听器组合在一起就可以帮助我们完成发送请求、验证结果及记录结果三项基本工作。


### Sampler「采样器」

### Logic Controller「控制器」
### Config Elements「配置元件」
### Timer「定时器」
### Assertions「断言」
### Listener「监听器」
### 「Pre」Post-processors 前置「后置」处理器 
## Thread Group「线程组」
## 总结
- 总结一
- 总结二
- 总结三


[项目演示地址]「https://github.com/testeru-pro/junit5-demo/tree/main/junit5-basic」
