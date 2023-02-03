# JMeter代理服务器录制Web端压测脚本

## 本章要点
1. 要点一
1. 要点
1. 要点
1. 要点

## 录制流程

### 压测对象

选用腾讯的[新闻](https://new.qq.com/)页面进行压测脚本的录制。

### 压测页面

涉及到的压测页面包括**三**个，分别是：腾讯**新闻首页**、新闻的**财经**页面、新闻的**科技**页面。


### 业务步骤

1. 打开浏览器，访问腾讯[新闻](https://new.qq.com/)页面。
2. 点击页面Tab栏中的[财经](https://new.qq.com/ch/finance/)跳转到财经新闻页面。
3. 点击页面Tab栏中的[科技](https://new.qq.com/ch/tech/)跳转到科技新闻页面。


以上为业务的功能测试流程。

### 录制步骤

下面来看下怎样使用`JMeter`的代理服务器来录制压测脚本。

#### 1. 命令行打开JMeter的GUI界面

默认创建测试计划，在界面上方对应当前`JMeter`版本号。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203144128.png)

#### 2. 保存脚本

当前界面的脚本默认没有保存，为了防止添加的组件及录制的脚本丢失，建议在打开了`GUI`界面后先对脚本进行保存。

脚本保存时，默认的文件名为测试计划组件的名称，选择好保存路径后，可在`File`对应的输入框内输入新的脚本文件名。

注意⚠️：要`jmx`结尾说明当前文件是一个`JMeter`脚本。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203145017.png)


脚本保存成功后，`JMeter`界面会显示文件名称及其路径。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203145110.png)

#### 3. 添加HTTP(S) 测试脚本记录器

第一个组件的添加，非测试组件。

导航到 测试计划(`Test Plan`) -> 添加(`Add`) -> 非测试元件(`Non-Test Elements`) -> HTTP 代理服务器(`HTTP(S) Test Script Recorder`)。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203155028.png)

`HTTP(S)` 测试脚本记录器允许 `JMeter` 在浏览器浏览 `Web` 应用程序时拦截并记录操作。

#### 4. 添加录制的请求路径组件

虽然添加了`HTTP(S)` 测试脚本记录器，但是记录下的来的`HTTP`请求还没有存放路径。下面来添加录制的请求存放路径组件。

##### 线程组组件

导航到 测试计划(`Test Plan`) -> 添加(`Add`) -> 线程(`Threads`) -> 线程组(`Thread Group`)。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203155118.png)

##### 添加录制控制器组件

导航到 线程组(`Thread Group`) -> 添加(`Add`) -> 逻辑控制器(`Logic Controller`) -> 录制控制器(`Recording Controller`)。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203155816.png)

录制控制器组件下会存放录制的脚本请求内容。

#### 5. 配置HTTP(S)测试脚本记录器

组件都添加完成后，需要对`JMeter`的录制控制器进行配置。

##### 监听端口配置

`Port`：设置监听浏览器的端口号，默认是8888。

注意⚠️：
端口号设置的前提是要求当前端口号在客户端**没有被占用**。

```bash
# Mac Linux
netstat -an|grep "端口号"
# Window
netstat -an|findstr "端口号"
```

如果命令行对应结果没有输出，则代表当前端口号没有被占用。

当有相关进程输出时，说明端口号被占用，此时需要修改，比如修改端口号为6666。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203163430.png)

##### 脚本存放路径设置

**目标控制器**：用来指定最终录制**生成的脚本的存放位置**。

>设置`JMeter`录制请求的路径，在 测试计划内容(`Test Plan Creation`) 下设置目标控制器。

点击下拉小三角可以看到目标控制器有**三**个选项，建议选择存放路径为：测试计划(`Test Plan`) -> 线程组(`Thread Group`) -> 录制控制器(`Recording Controller`)。

存放在录制控制器下**优点**：

1. 可以与其他编写的请求组件进行区分。

2. 要删除录制相关的请求组件时，直接删除该组件即可。

3. 录制的请求组件可直接在该节点下保存为新的测试计划。

##### 脚本编码格式设置

录制的页面是中文页面，中文应用一般使用的是`UTF-8`的编码格式。录制脚本时也需要声明编码格式与客户端的编码格式保持一致，否则会出现乱码问题。

`Recording's default encoding`：`JMeter`录制时的默认编码，中文应用设置为**utf-8**。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203165425.png)


##### 请求类型

`Type`：`HTTP`请求的实现类型，默认是`httpclient4`。

若录制时出现报错，解决方案为：考虑换成`java`模式。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203171924.png)

#### 6. 启动代理服务器

当所有配置检查完毕后，点击 **HTTP(S)测试脚本记录器** 组件的 启动`Start` 按钮，此时才会启动`JMeter`的代理服务器。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203172812.png)

##### 证书生成

启动之后会弹出根证书的提示信息。包含如下：
1. 根证书保存在`JMeter`的`bin`目录。
1. 根证书的有效期为**7**天。
1. 如果已安装了旧的根证书，确保删除旧证书并且安装新的。
    >说明证书安装至电脑端不会被覆盖。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203173054.png)

##### 证书验证

打开`{jmeter_path}/bin`路径下查看生成的证书是否存在。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203173327.png)

#### 7. 证书配置

##### Mac系统

###### 1. 导入

钥匙串访问 -> 系统 -> 文件 -> 导入项目，选择对应证书地址导入。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203175249.png)

###### 2. 信任
   
导入后发现对应证书未被信任。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203180154.png)

点开证书发现证书配置是使用系统默认，系统为了保证安全性，默认手动添加的证书都是不被信任的。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203180449.png)

修改完成后，直接关闭输入密码即可。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203180628.png)

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230203181717.png)

#### 7. 执行

#### 
## 总结
- 总结一
- 总结二
- 总结三


[项目演示地址](https://github.com/testeru-pro/junit5-demo/tree/main/junit5-basic)
