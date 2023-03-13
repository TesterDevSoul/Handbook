## Allure2 介绍

Allure2 是一个**开源**的测试报告框架，可以帮助测试人员和开发人员更好地**展示和管理测试结果**。它支持多种测试框架（如JUnit、TestNG、Cucumber、Pytest等）和多种编程语言（如Java、Python等），能够生成详细、易于理解的测试报告。

### 主要特点

Allure2 的主要特点包括：

##### 多样化的报告展示

Allure2 提供了多种报告展示方式，如饼图、散点图、韦恩图等，可以根据需要进行选择。

##### 支持历史记录

Allure2 支持将测试结果存储到数据库中，可以随时查看历史测试结果。

##### 支持多语言

Allure2 支持多种编程语言，可以在不同的开发环境中使用。

##### 易于集成

Allure2 可以与多种测试框架集成，包括JUnit、TestNG、Cucumber等，同时还可以与 CI/CD 工具（如Jenkins）进行集成。

##### 灵活的配置选项
Allure2 提供了多种配置选项，可以根据需要进行自定义配置。


总之，Allure2 是一个功能强大、易于使用的测试报告框架，可以帮助开发人员和测试人员更好地管理测试结果，提高测试效率和质量。


## Allure2 报告展示

## Allure2 安装

Allure2 安装有以下几种方式，不同的安装方式对应的配置内容不同：

1. 命令行工具安装。

2. 压缩包解压安装。

3. Python插件安装。

4. Maven插件安装。



要安装 Allure2，您需要完成以下步骤：

### 1. 环境准备

确保已安装 `Java` 环境，版本需要在 **1.8** 或以上。


### 方式1：命令行工具安装
安装 `Allure2` 命令行工具。

可以使用以下命令在终端中进行安装：
```bash
# for Linux
$ sudo apt-add-repository ppa:qameta/allure
$ sudo apt-get update 
$ sudo apt-get install allure

# for Mac
$ brew install allure

# for Windows
$ scoop install allure

```

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230310112323.png)


直接在命令行输入命令验证对应版本。
```bash
# 环境验证
allure --version
```

### 方式2：压缩包解压安装

压缩包下载方式有两种：

方式一：在 [Allure2 GitHub Release](https://github.com/allure-framework/allure2/releases) 页面下载对应操作系统版本的 `Allure2`。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230310113301.png)

方式二：在 [maven repo](https://repo1.maven.org/maven2/io/qameta/allure/allure-commandline/) 页面下载对应版本的 `Allure2`。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230310113043.png)

压缩包下载后，解压，将 `bin` 目录添加到环境变量中。

环境变量配置生效后，直接在命令行输入命令验证对应版本。
```bash
# 环境验证
allure --version
```

### 方式3：Python插件安装

安装`Allure Python`插件，需要先安装`Python`和`pip`包管理工具。

在安装前请确保在操作系统上安装了`Java`运行环境，因为`Allure`是用`Java`编写的。

以下是使用 `pip` 安装 `Allure Python` 插件的步骤：

1. 打开命令行终端。

2. 运行以下命令来安装 `Allure Python` 插件：

    ```bash
    pip install allure-pytest
    ```

3. 等待安装完成验证。

    ```python
    # linux/mac
    > pip list |grep allure
    allure-pytest         x.xx.x

    # windows
    > pip list |findstr allure
    allure-pytest         x.xx.x
    ```


### 方式4：Maven插件安装


要在`Maven`项目中安装`Allure`插件，需要在Maven项目的`pom.xml`文件中添加如下插件配置：

```xml
<properties>
    <allure.version>2.21.0</allure.version>
    <allure.maven.version>2.12.0</allure.maven.version>
    <allure.cmd.download.url>
        https://repo.maven.apache.org/maven2/io/qameta/allure/allure-commandline
    </allure.cmd.download.url>
</properties>



<build>
  <plugins>
    <plugin>
      <groupId>io.qameta.allure</groupId>
      <artifactId>allure-maven</artifactId>
      <version>${allure.maven.version}</version>
      <configuration>
        <!-- allure报告的版本号 -->
        <reportVersion>${allure.version}</reportVersion>
        <allureDownloadUrl>${allure.cmd.download.url}/${allure.version}/allure-commandline-${allure.version}.zip</allureDownloadUrl>
        <!-- <resultsDirectory>${project.build.directory}/allure-results</resultsDirectory>
        <reportDirectory>${project.build.directory}/allure-report</reportDirectory> -->
      </configuration>
    </plugin>
  </plugins>
</build>
```

其中，`<groupId>`指定了插件的`groupId`，`<artifactId>`指定了插件的`artifactId`，`<version>`指定了插件的版本号。`<configuration>`中可以配置一些参数，例如报告的版本号。

在添加了插件配置之后，可以使用以下`Maven`命令来生成`Allure`测试报告：

```bash
mvn clean allure:report
```

命令行运行以上命令，不用管中间是否有对应ERROR，运行完后在该项目下查看隐藏的文件夹是否有allure，在allure文件夹下有对应版本号的文件，说明当前项目下对应的allure版本下载成功。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230310160755.png)




```bash
mvn clean test
mvn allure:report

# 上面的命令也可以合并为一个命令
# 去下载相关的allure版本，到当前项目的.allure文件夹内
mvn clean test --alluredir=target/allure-results allure:report 
mvn clean test -Dtest=指定运行测试类 allure:report
```


##### mvn clean test 
将测试结果生成为`Allure`需要的json格式。`XML`格式的测试结果转换为`Allure`测试报告。
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230313165430.png)

##### mvn allure:report

会下载`allure`到本项目下，并且生成站点文件site。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230313165736.png)

```bash
# allure报告打开网站
mvn allure:serve
```

##### mvn allure:serve

启动一个本地服务器，可以在浏览器打开Allure报告。

生成的测试报告位于 `项目/target/site/allure-maven-plugin/index.html`，可以在浏览器中打开。


##### 注意⚠️

  使用命令行验证的前提是项目中有对应的测试用例，如果没有则无法生成对应的 allure-results 文件夹。


## Allure 运行原理


![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230310180336.png)

具体流程如下：

1. **测试用例** 代码编写并使用 **测试框架**「`JUnit5`」运行测试。

2. **测试执行器**「`JUnit5 执行器`」运行测试用例，然后将测试结果传递给 **Allure 测试监听器**「即`Allure JUnit5 扩展类`」。

3. **Allure 测试监听器**「即`Allure JUnit5 扩展类`」将测试用例结果转为测试报告所需的格式「测试结果 `XML` 文件」，并将其写入 **Allure 报告生成器**。<br>`mvn clean test`

    >maven 的 surefire插件 会将测试用例结果写入 **默认的报告文件夹下**「即`surefire-reports`」，生成**测试结果 XML 文件**「`surefire-reports/TEST-包名.类名`」。

    ![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230313162318.png)


4. **Allure 报告生成器**「`Allure命令行工具`」 读取测试结果 `XML` 文件，并根据测试结果 `XML` 文件生成 **Allure 报告文件夹**「`allure-result`」，其中包含 **测试结果** 和 **报告页面** 。<br>`mvn allure:report`


    ![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230313165736.png)

5. 打开浏览器，使用 Allure 报告文件夹中的页面查看生成的测试报告。<br>`mvn allure:serve`




需要注意的是，在 JUnit5 中使用 Allure 生成测试报告，需要在 Maven 或 Gradle 中添加 **Allure JUnit5 扩展类** 和 **Allure Maven/Gradle 插件** 的依赖
。

此外，还需要在测试类中添加 **Allure 的注解**，以便将测试结果写入 Allure 报告。


## 指定Allure路径

`--alluredir` 是插件「`Python`插件、`Maven Surefire`插件」提供的一个参数，
可以在`pytest`命令行使用也可以在`mvn`命令行终端使用。如下：

```bash
# pytest命令行使用
pytest --alluredir = report目录

# mvn命令行使用 maven插件安装
mvn clean test --alluredir = report目录
```

例如：

根据指定目录生成报告：
```bash
# pytest命令行使用
pytest --alluredir=./report

# mvn命令行使用
mvn clean test --alluredir=target/allure-results
```

运行的步骤：

1. `mvn` 命令清除项目以前生成的`target`目录。
2. 运行测试用例。
3. 生成的allure结果数据保存到 `target/allure-results` 目录中。

`target/allure-results` 目录**优点**：

每次运行测试用例都会生成新的报告目录，不会在已有的目录内进行测试用例的叠加。


生成报告后运行 `serve` 打开测试报告，如下：
```bash
allure serve report目录

# mvn 直接找target/allure-results目录
mvn allure:serve 
```
`allure serve` 前提条件为`allure`配置了全局环境变量。

例如：

```bash
# pytest
allure serve ./report
#mvn
allure serve target/allure-results

# mvn 直接找target/allure-results目录
mvn allure:serve 
```

该命令将启动一个本地服务器，可以在浏览器打开Allure报告。