---
theme: "league"
transition: "fade"
highlightTheme: "monokai"
slideNumber: false
title: "ok"
use: 
---

# JMeter安装及配置-Mac

---

## 目录
1. 前置条件
1. 命令行安装
1. 压缩包安装

---


## 前置条件

- `Java`的环境安装配置。
   - `Java`的版本必须是`Java 8+`。


![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230106140728.png)


---

### 1. 命令行brew安装
- `Mac`电脑上已经安装了`brew`命令行工具。
    ```bash
    brew --version
    ```
- 运行结果为：
    ```
    Homebrew 3.6.13
    Homebrew/homebrew-core (git revision 2787e0a5d5d; last commit 2022-12-04)
    Homebrew/homebrew-cask (git revision 7bd3fc7aa8; last commit 2023-01-11)
    ```


![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116111248.png)




---

### 1. 命令行brew安装

- 终端运行安装命令：
    ```bash
    bew install jmeter
    ```
- 安装路径查看：
  - 默认安装的路径为 **/usr/local/Cellar/jmeter/版本号**。

---

### 如何进行安装路径的查看？

1. 通过`which`进行`JMeter`目录的显示。

2. 打开目录的上一层文件，右键选择显示原项目。

3. 跳转到`JMeter`真正运行的代码路径下。


---


### 命令行卸载
- 只能卸载`brew`命令行安装的`JMeter`。
    ```bash
    brew uninstall jmeter
    ```

---


### 2. 压缩包安装
去[官网](https://jmeter.apache.org/download_jmeter.cgi)下载对应版本的`Apache JMeter`压缩包，并解压到当前电脑上指定路径即可。


![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116105918.png)

---

### 配置环境变量
- `JMETER_HOME`：为`JMeter`解压路径。


```bash
#-------- jmeter ----------
JMETER_HOME=/**/apache-jmeter-5.5

export JMETER_HOME
export PATH=$PATH:$JMETER_HOME/bin
```

---


## 界面化启动
JMeter无论是通过命令行安装还是通过压缩包解压安装，最后都需要通过界面化启动来验证。




![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230116143106.png)
