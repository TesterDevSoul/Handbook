# JUnit5基本注解 - All注解
## 本章要点
1. All 安装
1. All 运行原理
1. @BeforeAll 使用
1. @AfterAll 使用
1. All 计算器实战

## All 注解
### 安装
与@Test注解使用的是同一个依赖，不需要重新导入。
### 运行原理
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230104121305.png)

代码运行工具「IDE」运行`All`注解修饰的方法时通过`JUnit5`框架的`junit-jupiter`组件运行。


`@BeforeAll`注解其实就是告诉 `JUnit5` 框架需要在所有的方法**前**运行一次的代码。
`@AfterAll`注解其实就是告诉 `JUnit5` 框架需要在所有的方法**后**运行一次的代码。

### @BeforeAll 注解

#### 使用
`@BeforeAll`注解修饰的方法相当于**所有测试用例的前置条件**。

#### 1. 注解位置

1. `@BeforeAll`注解是方法上的注解。「注解位置」

>`@BeforeAll`注解修饰方法时，放在方法上方。

#### 2. 注解方法声明规则

1. `@BeforeAll`修饰的方法没有**返回值**并且为**静态方法**，即方法由`static`修饰且返回值类型为`void`。

2. `@BeforeAll`注解修饰的方法可以被继承。


#### 3. 注解运行规则

1. `@BeforeAll`修饰的方法在测试类里面运行一次，并且是在所有的方法之**前**运行一次，与其在代码中的前后顺序无关。「注解修饰方法运行顺序」

2. `@BeforeAll`注解修饰的方法不可直接运行。

#### 4. 注解方法内容

1. `@BeforeAll`注解修饰的方法内编写的内容为：所有的测试方法前需要运行的前置条件。「所有用例统一的前置条件编写」

>在所有的方法之前运行一次；所以，当前测试类先运行该方法，再去运行其它，无论有多少个Test注解修饰的方法，@BeforeAll只在测试类编译成功后运行一次，并且是**第一个**运行。

#### 5. 注解个数

1. 一个测试类里可以有多个`@BeforeAll`注解修饰的方法，但是不建议使用。

#### Hello @BeforeAll
```java
public class AnAllTest {
    static final Logger logger = getLogger(lookup().lookupClass());

    @AfterEach
    public void afterEach(){
        logger.info("Every @Test After run...");
    }
    @Test
    public void one(){
        int result = 8 / 4;
        logger.info("Result：{}",result);
        assertEquals(2,result);
        logger.info("assertEquals is True");
    }
    @Test
    public void two(){
        int result = 2 + 8;
        logger.info("Sum Result：{}",result);
        assertEquals(10,result);
        logger.info("assertEquals is True");
    }
    @BeforeEach
    public void beforeEach(){
        logger.info("Every @Test Before run...");
    }
    @BeforeAll
    public static void beforeAll(){
        logger.info("All Annotation Before run...");
    }
}
```
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230224143429.png)

注意⚠️：
- `@BeforeAll`注解修饰的方法在代码的最后，但是在类运行所有的方法之前进行了打印。

#### 作用
- 测试用例中，**测试类**需要**初始化**的内容及属性：
  - 测试对象的声明：Webdriver ;AppiumDriver;  ChromeDriver
  - log日志删除；
  - apk包的安装；
  - 启动的某些参数的配置。

### @AfterAll 注解

#### 使用
`@AfterAll`注解修饰的方法相当于**所有测试用例的后置条件**。

#### 1. 注解位置

1. `@AfterAll`注解是方法上的注解。

>`@AfterAll`注解修饰方法时，放在方法上方。

#### 2. 注解方法声明规则

1. `@AfterAll`修饰的方法没有**返回值**并且为**静态方法**，即方法由`static`修饰且返回值类型为`void`。2. `@AfterAll`注解修饰的方法可以被继承。
#### 3. 注解运行规则

1. `@AfterAll`修饰的方法在测试类里面运行一次，并且是在所有的方法之**后**运行一次，与其在代码中的前后顺序无关。「注解修饰方法运行顺序」

1. `@AfterAll`注解修饰的方法不可直接运行。

#### 4. 注解方法内容

1. `@AfterAll`注解修饰的方法内编写的内容为：所有的测试方法后需要运行的后置条件。「所有用例统一的后置条件编写」

>在所有的方法之后运行一次；所以，当前测试类运行完所有方法之后，再去运行其它，无论有多少个Test注解修饰的方法，@AfterAll只在测试类编译成功后运行一次，并且是**最后**一个运行。

#### 5. 注解个数

1. 一个测试类里可以有多个`@AfterAll`注解修饰的方法，但是不建议使用。

#### Hello @AfterAll
```java
public class AnAllTest {
    static final Logger logger = getLogger(lookup().lookupClass());
    @AfterAll
    public static void afterAll(){
        logger.info("All Annotation After run...");
    }
    @AfterEach
    public void afterEach(){
        logger.info("Every @Test After run...");
    }
    @Test
    public void one(){
        int result = 8 / 4;
        logger.info("Result：{}",result);
        assertEquals(2,result);
        logger.info("assertEquals is True");
    }
    @Test
    public void two(){
        int result = 2 + 8;
        logger.info("Sum Result：{}",result);
        assertEquals(10,result);
        logger.info("assertEquals is True");
    }
    @BeforeEach
    public void beforeEach(){
        logger.info("Every @Test Before run...");
    }
    @BeforeAll
    public static void beforeAll(){
        logger.info("All Annotation Before run...");
    }
}
```
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230224144041.png)

注意⚠️：
- `@AfterAll`注解修饰的方法在代码的最上，但是所有的方法运行完后输出打印了@AfterAll对应内容。

#### 作用
- 测试用例中，**测试类**需要**销毁**的内容及属性：
  - apk卸载；
  - app退出；
  - 测试用例结束；
  - web端关闭浏览器操作；
  - 关闭数据库连接。


### All注意
`@BeforeAll` + `@AfterAll`可以同时修饰一个方法。


### BUG
#### All注解对应方法报错
```
org.junit.platform.commons.JUnitException: @BeforeAll method 'public void top.testeru.basic.AnAllTest.beforeAll()' must be static unless the test class is annotated with @TestInstance(Lifecycle.PER_CLASS).
```

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230105161106.png)


```
org.junit.platform.commons.JUnitException: @AfterAll method 'public void top.testeru.basic.AnAllTest.afterAll()' must be static unless the test class is annotated with @TestInstance(Lifecycle.PER_CLASS).
```
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230105161520.png)


##### 原因

`@BeforeAll`注解、`@AfterAll`注解 对应方法没有使用`static`关键字修饰导致错误。

##### 解决
`@BeforeAll`注解、`@AfterAll`注解对应方法使用`static`关键字声明。

## 总结
- `All`注解使用
  1. `@BeforeAll`、`@AfterAll`注解修饰的**方法不可直接运行**。
  2. `@BeforeAll`、`@AfterAll`注解可同时修饰一个方法。
  3. `@BeforeAll`、`@AfterAll`注解修饰的方法**static修饰**并且**没有返回值**，即方法声明时为`static void`。
  4. `@BeforeAll`、`@AfterAll`注解都可被继承。
  5. `@BeforeAll`注解在类的所有方法之**前**运行；`@BeforeAll`注解注解在类的所有方法之**后**运行，**无论断言是否失败**。
   


[项目演示地址](https://github.com/TesterDevSoul/Tutorials/blob/master/junit5-basic/src/test/java/top/testeru/basic/AnAllTest.java)
