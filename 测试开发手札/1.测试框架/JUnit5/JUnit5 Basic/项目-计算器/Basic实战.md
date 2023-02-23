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

### 涉及知识点

|知识点|备注|
|:-:| --- |
|[@Test注解](/archives/junit07)|使用@Test注解创建测试用例|
|[基本断言-assertEquals](/archives/junit08)|assertEquals()参数及各个含义|





![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230223120127.png)


### 计算器测试用例
#### 被测系统

```java
public class MySUT {
    //获得具有所需名称的记录器
    static final Logger logger = getLogger(lookup().lookupClass());

    String name;//用例名

    public MySUTOne(String name) {
        this.name = name;
        logger.info("Open {} ", name);
    }

    //连续添加
    public int sum(int... numbers) {
        if(Arrays.stream(numbers).anyMatch(u -> u == 100) | Arrays.stream(numbers).anyMatch(u -> u == -100)){
            //
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

#### 加法正向测试用例
##### 步骤
1. 被测系统计算器创建并命名：`My Basic Test Project`
2. 日志打印开始测试：`Begin Sum Test`
3. 测试用例步骤调用
4. 日志打印计算结果：`Sum Result：`

##### 代码
```java
package top.testeru.num;

/**
 * @author www.testeru.top
 * @version 1.0.0
 * @Project junit5-modules
 * @Description 加法功能的测试用例
 * @createTime 2023年02月23日 11:26:47
 */

import org.junit.jupiter.api.Test;
import org.slf4j.Logger;
import top.testeru.MySUT;

import static java.lang.invoke.MethodHandles.lookup;
import static org.junit.jupiter.api.Assertions.*;
import static org.slf4j.LoggerFactory.getLogger;

/**
 * 1. 创建加法计算器对象 -- new有参构造，传入参数值为：加法计算器
 * 2. 生成唯一ID
 * 3. log日志打印：开始进行{}计算,加法
 * 4. 业务逻辑调用，返回结果声明为result  [2+8=10]   [4+3+8=15]   [100+0=100]  [-100+8=-92]
 * 5. log日志打印计算结果：计算结果为{},result
 * 6. 销毁ID操作
 * 7. 计算的结果断言 -- assertEquals()，断言失败msg：2+8计算错误
 */
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
点击测试方法左侧运行按钮，只运行当前测试方法，输出结果如下：
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230104145755.png)

>可以创建多个测试方法sum，分别为:sum1()、sum2()、sum3()、sum4()<br>
>运行顺序为：sum1()、sum2()、sum3()、sum4()；与方法所在前后位置无关

## 总结
- 总结一
- 总结二
- 总结三


[项目演示地址](https://github.com/testeru-pro/junit5-demo/tree/main/junit5-basic)

