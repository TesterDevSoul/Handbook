# 文章名
## 本章要点
1. 要点一
1. 要点
1. 要点
1. 要点


## 计算器系统说明

计算器系统为`MySUT`类，其中有加法功能对应的方法为`sum()`。`sum()`方法为带参的方法，可以是传入**一个int类型的参数**，也可以传入**多个int类型的参数**，还可以直接传入**一个int[]数组**。

当传入**一个int类型参数**时，就是int默认的参数值0加上传入的值。

当传入的参数包含 **100** 时，报错。错误类型为：`NumberFormatException`，对应的提示信息为：`Enter an integer is 100！`

当传入的参数其中一个 **>99** 或者 **<-99** 时，报错。错误类型为：`IllegalArgumentException`，对应的提示信息为：`Please enter an integer in the range!`

每次进行计算前，计算器都会默认生成唯一ID，即`initId()`方法。在计算结果得出后，生成的ID需要销毁，即`destroyId()`方法。

- `sum()`：加法，连续加
  - 可以传入参数为单个`int`也可以为数组`int[]`
  - 如果传入的参数为**100**，报错
    - 错误类型：`NumberFormatException`
    - 错误信息：`Enter an integer is 100！`
  - 如果传入的参数 **>99** 或者 **<-99**，报错
    - 错误类型：`IllegalArgumentException`
    - 错误信息：`Please enter an integer in the range!`

## 阶段一

### 被测代码
```java
import org.slf4j.Logger;
import java.util.Arrays;
import java.util.UUID;
import java.util.stream.IntStream;
import static java.lang.invoke.MethodHandles.lookup;
import static org.slf4j.LoggerFactory.getLogger;


public class MySUT {
    //获得具有所需名称的记录器
    static final Logger logger = getLogger(lookup().lookupClass());
    //用例名
    String name;
    //唯一ID标识
    String id;

    public MySUT(String name) {
        this.name = name;
        logger.info("Open {} ", name);
    }
    public void initId(){
        id = UUID.randomUUID().toString();
        logger.info("Generate ID：{} ", id);
    }
    public void destroyId() {
        if (id == null) {
            throw new IllegalArgumentException(name + " 没有初始化对应ID");
        }
        logger.info("Release ID: {} ", id);
        id = null;
    }

    public void close() {
        logger.info("Close {} ", name);
    }

    //连续添加
    public int sum(int... numbers) {
        if(Arrays.stream(numbers).anyMatch(u -> u == 100) | Arrays.stream(numbers).anyMatch(u -> u == -100)){
            //输入100
            logger.warn("Enter an integer is 100！");
            throw new NumberFormatException("Enter an integer is 100！");
        }else if (Arrays.stream(numbers).anyMatch(u -> u > 99) |
                Arrays.stream(numbers).anyMatch(u -> u < -99)){
            // 请输入范围内的整数
            logger.warn("Please enter an integer in the range!");
            throw new IllegalArgumentException("Please enter an integer in the range!");
        }else {
            return IntStream.of(numbers).sum();
        }
    }

}
```


### 测试准备

根据被测代码编写相关测试用例。

[加法测试用例](加法测试用例.xlsx)


![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230223170046.png)

idea创建maven项目，导入JUnit5相关依赖，声明对应测试类为**SumTest**。

### sumOne

测试方法为**sumOne()**。

#### 步骤
1. 创建加法计算器对象。
2. 生成唯一ID。
3. log日志打印：`开始进行{}计算,加法`。
4. 业务逻辑调用，返回结果声明为result。
5. log日志打印计算结果：`计算结果为{},result`。
6. 销毁ID操作。
7. 计算的结果断言。


#### 涉及知识点

|知识点|备注|
|:-:| --- |
|[@Test注解](/archives/junit07)| 1. @Test注解是方法上的注解。<br>2. 一个测试类中可以有多个测试方法，即多个@Test注解修饰的方法。<br>3. @Test注解修饰的方法返回值类型是void。<br>4. @Test注解修饰的方法的内容是测试用例执行的具体内容及断言结果。|
|[assertEquals](/archives/junit08)|1. assertEquals()可以有2个参数，也可以有3个参数。<br>2.参数分别为：<br>&nbsp;&nbsp;&nbsp;&nbsp;expected「期望值」;<br>&nbsp;&nbsp;&nbsp;&nbsp;actual「实际值」;<br>&nbsp;&nbsp;&nbsp;&nbsp;message「断言失败提示语」。|

#### 示例代码

- 【正向】整数相加，结果计算正确


```java
public class SumTest {
    static final Logger logger = getLogger(lookup().lookupClass());

    // 2+8=10
    @Test
    public void sumOne(){
        //1. 创建加法计算器对象 -- new有参构造，传入参数值为：加法计算器
        MySUT mySUT = new MySUT("Sum Calculator");
        //2. 生成唯一ID
        mySUT.initId();
        //3. log日志打印：开始进行{}计算,加法
        logger.info("Start adding...");
        //4. 业务逻辑调用，返回结果声明为result
        int result = mySUT.sum(2, 8);
        //5. log日志打印计算结果：计算结果为{},result
        logger.info("Calculated as: {}", result);
        //6. 销毁ID操作
        mySUT.destroyId();
        //7. 计算的结果断言 -- assertEquals()，断言失败msg：2+8计算错误
        /**
         * expected   期望值，10
         * actual     实际值，result
         * message    断言失败原因的解释说明，2+8计算错误
         */
        assertEquals(10, result, "2+8计算错误");
    }
}
```

### sumBoundaryErrorOne

测试方法为**sumBoundaryErrorOne()**。

#### 步骤
1. 创建加法计算器对象。
2. 生成唯一ID。
3. log日志打印：`开始进行{}计算,加法`。
4. 计算的异常结果断言，返回异常声明为exception。
5. 销毁ID操作。
6. 异常的提示语断言。

#### 涉及知识点

|知识点|备注|
|:-:| --- |
|[assertThrows & assertThrowsExactly](/archives/junit08)||

#### 示例代码
- 【边界】无效边界值相加，抛出异常并断言提示信息


```java
    @Test
    public void sumBoundaryErrorOne(){
        //1. 创建加法计算器对象 -- new有参构造，传入参数值为：加法计算器
        MySUT mySUT = new MySUT("Sum Calculator");
        //2. 生成唯一ID
        mySUT.initId();
        //3. log日志打印：开始进行{}计算,加法
        logger.info("Start adding...");
        //4. 计算的结果断言
        /**
         * 异常断言：
         * assertThrows「抛出异常或异常的父类」：   expectedType  抛出的异常类型；   executable    异常业务
         * assertThrowsExactly「抛出当前异常类」
         */
        /*Exception throwException = assertThrows(
                                        RuntimeException.class,
                                        () -> mySUT.sum(100, 1));*/
//        Exception exception = assertThrowsExactly(RuntimeException.class, () -> mySUT.sum(100, 1));
        Exception exception =assertThrowsExactly(
                                        NumberFormatException.class,
                                        () -> mySUT.sum(100, 1));

        mySUT.destroyId();
        //5、异常信息提示语验证
        //assertTrue(exception.getMessage().contains("enter an integer in the range"));
        assertEquals("Enter an integer is 100！",exception.getMessage());
    }
```

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230223174526.png)


## 阶段二

重复代码进行优化。创建基本类BaseTest，使测试类继承BaseTest。
把一些重复的代码提取出来放在BaseTest中。
### Before

每次业务逻辑相关测试代码运行前要运行的步骤，提取出来。

如果是只运行一次，则提取到@BeforeAll注解修饰的方法里面。

如果是需要在每个测试方法之前都要运行一次，则提取到@BeforeEach注解修饰的方法内。
#### 步骤
1. BaseTest

## 总结
- 总结一
- 总结二
- 总结三


[项目演示地址](https://github.com/testeru-pro/junit5-demo/tree/main/junit5-basic)

