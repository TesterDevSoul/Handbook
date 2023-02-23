# 测试用例断言 - assertEquals
## 本章要点
1. 断言概念&步骤
1. assertEquals()方法参数


## 断言概念

测试用例通过测试的步骤进行验证后，需要查看执行完测试步骤后的结果即**实际值**和**期望结果**（`Expectation vs Reality`）是否一致。

### 测试用例基本步骤

1. 创建被测类的实例
2. 编写业务逻辑的代码       
3. 使用断言验证结果是否符合您的预期


### 注意⚠️

1. 断言没有返回值，返回值类型为`void`。
   
2. 断言通过，说明当前的业务逻辑对应的测试用例通过。
   
3. 断言通过后，断言后的代码正常运行。

4. 断言失败后，断言后的代码不会运行。



## assertEquals( )

`assertEquals()`方法为判断两个对象是否相等，如果相等则结果为`true`，否则为`false`。
>类似于字符串比较使用的`equals()`方法，但是断言没有返回值。如下图，无论`assertEquals()`方法内传入的参数类型是什么，最终的方法返回值都是`void`。

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230104154120.png)


### 参数

常用的参数传入有三个，expected、actual、message。

#### expected
期望值。希望当前方法中业务逻辑运行的结果。

#### actual
实际值。当前方法在执行完业务逻辑后的实际结果。

#### message
如果期望值和实际值不相同，即断言失败对应显示的提示内容。

#### messageSupplier
生产者接口。



#### 两个参数

当`assertEquals()`传入2个参数时，只是断言当前方法运行的预期结果和实际结果是否相等。

```java
assertEquals(expected, actual)
```
`expected` & `actual`参数类型可以是Java的 **八大基本数据类型**及其**包装类**，还可以是 **Object类**。其中，Object是Java所有类的父类。也就是，`expected` & `actual`参数类型可以是任意对象。


### 三个参数

当`assertEquals()`传入3个参数时，不只是断言当前方法运行的预期结果和实际结果是否相等，还可以在断言失败时提供失败的提示消息。

当为预期值和实际值提供相同的对象时「八大基本数据类型及其包装类」， `assertEquals()` 会立即返回判断的结果，根本不调用 `equals(Object)`

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230223161036.png)

#### String
```java
assertEquals(expected, actual, String message)
```
`message`的参数类型只能是 `String`。

#### `Supplier<String>`
```java
assertEquals(expected, actual, Supplier<String> messageSupplier)
```
`messageSupplier`的参数类型是`Supplier`类。从提供的 `messageSupplier` 延迟检索失败消息。

Supplier接口定义了一个 T get() 的抽象方法。
其函数描述符为 `() -> T`。如果不接受入参，直接为我们生产一个指定的结果，那么就可以用`Supplier<T>`。


#### `Supplier<String> vs String`

`String`类型的`message`里面的内容无论断言是否失败，都会运行。`Supplier<String>`的`messageSupplier`代码，只有在断言失败的时候才会运行。
### 示例代码
#### 断言通过
```java
    @Test
    public void sum() {
        int result = 2 + 8;
        logger.info("Sum Result：{}",result);
        //2个参数 -- 断言成功
        //Assertions.assertEquals(10,result);
        assertEquals(10,result);
    }
```

点击测试方法左侧运行按钮，只运行当前测试方法，输出结果如下：

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230223162848.png)


#### 断言失败String
```java
    @Test
    public void sum1() {
        int result = 2 + 1;
        logger.info("\n Sum Result：{}",result);
        //3个参数 -- String 断言失败
        //Assertions.assertEquals(10, result, "2 + 1运算失败");
        assertEquals(10,result, "2 + 1运算失败");
        logger.info("\n assertEquals is Fail");
    }
```

点击测试方法左侧运行按钮，只运行当前测试方法，**断言后的日志信息**没有被打印，输出结果如下：

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/1677141325076.png)

#### 断言失败Supplier


```java
    @Test
    public void sumFailWithSupplier() {
        //1、被测系统命名为 - My Basic Test Project
        MySUT mySUT = new MySUT("My Basic Test Project");
        //2、打印日志 - Begin Sum Test
        logger.info("Begin Sum Test");
        //3、测试用例步骤调用 - sum()
        int result = mySUT.sum(4, 1);
        //4、打印结果日志 - Sum Result
        logger.info("Sum Result：{}",result);
        int expected = 7;
        //5、测试用例结果验证
        //expected:期望值,  actual:运算的实际值
        assertEquals(expected,result, ()->"4+1计算结果为："+result+"，期望结果为："+expected);
        logger.info("断言失败");
    }
```

点击测试方法左侧运行按钮，只运行当前测试方法，**断言后的日志信息**没有被打印，输出结果如下：

![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230223163842.png)

## 总结
- 断言概念
- assertEquals()参数含义


[项目演示地址](https://github.com/TesterDevSoul/Tutorials/blob/master/junit5-modules/junit5-basic/src/test/java/top/testeru/basic/An_01AssertEquals_Test.java)