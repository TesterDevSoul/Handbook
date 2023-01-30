# JMeter安装及配置-Mac

## 本章要点
1. 前置条件
1. 命令行安装
1. 压缩包安装


在`Mac`上安装对应的`JMeter`工具有两种方式：一种直接借助**终端命令行**`brew`进行安装；另外一种和`Window`电脑一样去`JMeter`官网下载**压缩包安装**。

无论是哪种安装方式，都需要有对应环境的前置条件，下面先来看一下对应的前置条件：

## 前置条件
### Java安装配置

1. 在安装`JMeter`之前，要把`Java`的环境安装配置成功。由于`JMeter`使用的是`Java`语言进行开发的一个应用，所以运行`JMeter`的前提当前机器有`Java`环境。`Java`的版本必须是**Java 8+**，本文使用的是`jdk11`。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230106140728.png)

## 方式一：命令行brew安装
### 准备

使用命令行`brew`进行安装的前提是：`Mac`电脑上已经安装了`brew`命令行工具。

可以在命令行输入以下命令进行验证：
```bash
brew --version
```
对应的运行结果为：
```
Homebrew 3.6.13
Homebrew/homebrew-core (git revision 2787e0a5d5d; last commit 2022-12-04)
Homebrew/homebrew-cask (git revision 7bd3fc7aa8; last commit 2023-01-11)
```
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116111248.png)

### brew安装JMeter

终端显示对应`brew`的版本号后，即可在命令行终端运行`brew`的安装命令：

```bash
bew install jmeter
```

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230130150002.png)

### 安装路径查看

命令行安装的默认安装的路径为`/usr/local/Cellar/jmeter/版本号`。

本次安装的是5.5的版本，所以安装路径为：`/usr/local/Cellar/jmeter/5.5`。

下面来进行路径的查看及验证。

#### 如何进行安装路径的查看？

**步骤**：

1. 通过命令`which`进行`JMeter`目录的显示。
   ```bash
   which jmeter
   ```
   ![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230130150200.png)

2. 打开目录的上一层文件，右键选择显示原项目。
    ![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116135447.png)

3. 跳转到`JMeter`真正运行的代码路径下。
    ![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116140257.png)



### 启动

命令行安装的`JMeter`**无需配置环境变量**，在命令行输入`jmeter`即可打开`GUI`界面。

```bash
jmeter
```

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116143106.png)


### 卸载

如果需要卸载，则直接在命令行输入以下命令：

```bash
brew uninstall jmeter
```

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230130150241.png)


注意⚠️：只能卸载`brew`命令行安装的`JMeter`。

## 方式二：官网安装JMeter

如果是要压缩包进行解压安装，则需要打开[官网](https://jmeter.apache.org/download_jmeter.cgi)。

### 压缩包下载

1. [官网](https://jmeter.apache.org/download_jmeter.cgi)下载对应版本的`Apache JMeter`压缩包。
   
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116105918.png)

### 解压

2. 下载的压缩包解压到当前电脑的指定路径即可。本篇文章直接解压到当前用户目录下，如下所示：

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230106140822.png)



### 配置环境变量
此时，虽然安装成功，但是需要对`JMeter`进行环境变量的配置，否则，无法直接使用命令行启动`JMeter`的界面化。

```bash
#-------- jmeter ----------
JMETER_HOME=/**/apache-jmeter-5.5

export JMETER_HOME
export PATH=$PATH:$JMETER_HOME/bin
```
- `JMETER_HOME`：为`JMeter`解压路径。

>配置完环境变量后，在终端需要`source`保存后再**重新打开**命令行窗口才可生效。

### 启动
JMeter无论是通过命令行安装还是通过压缩包解压安装，最后都需要通过界面化启动来验证。

```bash
jmeter
```

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116143106.png)

界面化可以启动成功，则说明对应Mac电脑安装`JMeter`成功。

### 卸载

直接删除解压的文件夹即可卸载，无需过多操作。当环境变量中找不到该路径，对应则不生效。

## 总结
- 压缩包安装需要配置环境变量，才可使用命令行启动。
- 命令行安装`JMeter`可直接终端输入命令启动。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230130151516.png)