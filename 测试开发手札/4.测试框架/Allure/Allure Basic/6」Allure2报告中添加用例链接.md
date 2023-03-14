
## Allure2 报告中添加用例链接

### 应用场景

在测试过程中，有时候需要将测试用例与其他相关资源进行关联，例如：

#### 1. Bug跟踪工具

测试人员在测试过程中，可能会发现一些软件缺陷或者`bug`，需要将这些问题记录到Bug跟踪工具中。此时，可以使用@Link注解将当前测试用例与对应的Bug进行关联，方便测试人员跟踪问题的解决情况。

#### 2. 需求跟踪工具

在软件开发过程中，需求文档通常都是使用需求跟踪工具进行管理的。如果测试人员发现了一个与某个需求相关的问题，可以使用@Link注解将测试用例与对应的需求进行关联，方便开发人员了解问题的背景和上下文。

#### 3. 文档

测试人员在测试过程中，可能会涉及到一些文档，例如测试计划、测试报告等。此时，可以使用@Link注解将测试用例与对应的文档进行关联，方便测试人员查看和管理文档。

通过使用`@Link`注解，可以将测试用例与其他相关资源进行关联，帮助测试人员更好地进行测试管理和问题跟踪。同时，在`Allure2`报告中，也可以方便地查看和跳转到相关资源，提高测试过程的效率和准确性。


## 添加用例链接的方式

1. 使用`@Link`注解。
    >`@Link`注解是`Allure`提供的一种注解，可以用来在测试报告中添加链接。<br>通过在测试方法上添加`@Link`注解，可以为**测试用例添加链接**，并在测试报告中展示出来。

2. 使用`Allure.addLink()`方法。
    >除了使用`@Link`注解之外，还可以在测试方法中使用`Allure.addLinkv`方法来添加链接。<br>与`@Link`注解不同的是，`Allure.addLink()`方法可以 **动态添加链接**，并且可以 **添加多个链接**。

### 注解方式添加

@Link注解用于将外部资源链接到测试用例中，例如：bug跟踪工具、需求跟踪工具等。

步骤的代码示例：

```java
public class LinkAnTest {
    //使用@Link注解为测试用例添加了一个名为“百度首页”的链接，
    //链接的类型为“mylink”
    // 链接地址为“https://www.baidu.com/”。
    @Link(name = "百度首页", type = "mylink", url = "https://www.baidu.com/")
    @Test
    public void testBaiduHomePage(TestInfo testInfo) {
        Link link = testInfo.getTestMethod().get().getAnnotation(Link.class);
        String name = link.name();
        String url = link.url();
        System.out.println("name:" +name);
        System.out.println("url:" +url);
        assertEquals("https://www.baidu.com/", url, name + "错误");
    }
}
```
>使用反射获取了当前测试方法上的`@Link`注解，并获取了注解中的**名称**和**链接**地址。<br>需要注意的是，获取**注解内容**时需要使用**Java反射机制**，即通过 **Class和Method对象来获取注解内容**。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230314175055.png)

在`Allure2`报告中，将会显示一个“`Links`”部分，包含了链接名称，用户可以通过点击链接跳转到指定的`URL`。

需要注意的是，如果需要在 **测试类的多个测试方法中使用同一个链接**，可以将`@Link`注解添加到测试类上，而不是每个测试方法中。

例如：
```java
@DisplayName("链接添加验证")
@Link(name = "腾讯首页", type = "mylink", url = "https://www.qq.com/")
public class LinkAnTest {
    @Link(name = "百度首页", type = "mylink", url = "https://www.baidu.com/")
    @Test
    public void testBaiduHomePage(TestInfo testInfo) {
        Link link = testInfo.getTestMethod().get().getAnnotation(Link.class);
        String name = link.name();
        String url = link.url();
        System.out.println("name:" +name);
        System.out.println("url:" +url);
        assertEquals("https://www.baidu.com/", url, name + "错误");
    }
    @Test
    public void testAdd() {
        int result = 8 + 9;
        assertEquals(17,result,"8 + 9的计算结果失败");
    }
}
```
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230314175517.png)




将@Link注解添加到了测试类上，这将为测试类中的所有测试方法添加同一个链接。

### 方法直接添加

`Allure.addLink()`方法是`Allure`框架提供的一个方法，用于在测试报告中添加链接。该方法可以**动态添加链接**，并且可以**添加多个链接**。