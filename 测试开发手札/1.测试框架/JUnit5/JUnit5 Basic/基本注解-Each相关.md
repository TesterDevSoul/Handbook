# JUnit5基本注解-Each相关
## 本章要点
1. Each 安装
1. Each 运行原理
1. @BeforeEach 使用
1. @AfterEach 使用
1. Each 计算器实战

## Each 注解
### 安装
与`@Test`注解使用的是同一个依赖，不需要重新导入。
### 运行原理
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230104121305.png)

代码运行工具「IDE」运行`Each`注解修饰的方法时通过`JUnit5`框架的`junit-jupiter`组件运行。


`@BeforeEach`注解其实就是告诉 `JUnit5` 框架需要在每个`@Test`注解方法**前**需要运行哪些代码。

`@AfterEach`注解其实就是告诉 `JUnit5` 框架需要在每个`@Test`注解方法**后**需要运行哪些代码。

## @BeforeEach 注解

### 使用

`@BeforeEach`注解修饰的方法相当于**每个测试方法的前置条件**。

#### 1. 注解位置

1. `@BeforeEach`注解是方法上的注解。

>`@BeforeEach`注解只可修饰方法，放在方法上方。`@BeforeEach`注解不可修饰类。

#### 2. 注解方法声明规则

1. `@BeforeEach`修饰的方法没有**返回值**，即返回值类型为`void`。


#### 3. 注解运行规则

1. `@BeforeEach`修饰的方法是在每一个`@Test`注解修饰方法之**前**运行，与其在代码中的前后顺序无关。「注解修饰方法运行顺序」
   
2. `@BeforeEach`注解修饰的方法不可直接运行。

#### 4. 注解方法内容

1. `@BeforeEach`注解修饰的方法内编写的内容为：每一个测试方法前需要运行的前置条件。「用例前置条件编写」

>在每一个@Test注解修饰的方法之前运行一次；所以，当前测试类有多少个@Test注解，@BeforeEach注解修饰的方法就运行多少次。

注解作用：

测试用例中，测试方法需要初始化的内容及属性。比如：app/web端进入固定页面，回退到固定页面；重启app；删除某些产生的测试数据。


#### 5. 注解个数

1. 一个测试类里可以有多个`@BeforeEach`注解修饰的方法，但是不建议使用。「注解个数」

### Hello @BeforeEach
```java
public class AnEachTest {
    static final Logger logger = getLogger(lookup().lookupClass());
    
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
}
```
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230224142513.png)

注意⚠️：
- `@BeforeEach`注解修饰的方法在代码的最后，但是每个测试方法前都输出打印了对应内容。

### 作用
- 测试用例中，**测试方法**需要**初始化**的内容及属性：
  - UI自动化中需要进入固定页面，回退到固定页面；
  - App自动化中的每个阶段用例需要重启app；
  - 自动化测试中需要提前删除由于测试产生的测试数据。

## @AfterEach 注解
#### 使用

`@AfterEach`注解修饰的方法相当于**每个测试方法的后置条件**。

#### 1. 注解位置

1. `@AfterEach`注解是方法上的注解。

>`@AfterEach`注解修饰方法时，放在方法上方。

#### 2. 注解方法声明规则

1. `@AfterEach`修饰的方法没有**返回值**，即返回值类型为`void`。


#### 3. 注解运行规则

1. `@AfterEach`修饰的方法是在每一个`@Test`注解修饰方法之**后**运行，与其在代码中的前后顺序无关。

2. `@AfterEach`注解修饰的方法不可直接运行。

3. 无论`@Test`注解修饰的测试方法是否断言成功，`@AfterEach`注解修饰的方法都会运行。

>`@Test`注解修饰方法哪怕断言失败，`@AfterEach`的内容也会运行。

#### 4. 注解方法内容

1. `@AfterEach`注解修饰的方法内编写的内容为：每一个测试方法后需要运行的后置条件。「用例后置条件编写」

>在每一个@Test注解修饰的方法之后运行一次；所以，当前测试类有多少个@Test注解，@AfterEach注解修饰的方法就运行多少次


#### 5. 注解个数


1. 一个测试类里可以有多个`@AfterEach`注解修饰的方法，但是不建议使用。


### Hello @AfterEach
```java
public class AnEachTest {
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
}
```
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230224142716.png)

注意⚠️：
- `@AfterEach`注解修饰的方法在代码的最前，但是每个测试方法后都输出打印了对应内容。


### 作用
- 测试用例中，**测试方法**需要**销毁**的内容及属性：
  - UI自动化中需要返回首页，返回固定页面；
  - App自动化中的每个阶段用例需要退出app；
  - 删除/销毁产生的测试数据。

### Each注意

`@BeforeEach` + `@AfterEach`可以同时修饰一个方法。


## 总结
- `Each`注解使用
  1. `@BeforeEach`、`@AfterEach`注解修饰的方法不可直接运行
  2. `@BeforeEach`、`@AfterEach`注解可同时修饰一个方法
  3. `@BeforeEach`、`@AfterEach`注解修饰的方法没有返回值，即方法声明时为`void`
  4. `@BeforeEach`注解在每个`@Test`之**前**都运行一次；`@AfterEach`注解在每个`@Test`之**后**都运行一次，**无论断言是否失败**；


[项目演示地址](https://github.com/TesterDevSoul/Tutorials/blob/master/junit5-basic/src/test/java/top/testeru/basic/AnEachTest.java)
