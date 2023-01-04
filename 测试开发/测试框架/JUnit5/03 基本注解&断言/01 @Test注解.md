# JUnit5基本注解 - @Test注解
## 本章要点
1. 要点一
1. 要点
1. 要点
1. 要点

## @Test注解


### 安装

```xml
<properties>
    <maven.compiler.encoding>UTF-8</maven.compiler.encoding>
    <maven.compiler.version>3.8.1</maven.compiler.version>
    <maven-surefire-plugin.version>3.0.0-M7</maven-surefire-plugin.version>
    <java.version>17</java.version>
    <!-- 对应junit Jupiter的版本号;
    放在这里就不需要在每个依赖里面写版本号，导致对应版本号会冲突 -->
    <junit.jupiter.version>5.9.1</junit.jupiter.version>
    <!-- log日志 -->
    <slf4j.version>2.0.5</slf4j.version>
    <logback.version>1.4.5</logback.version>
</properties>
<!--    物料清单 (BOM)-->
<dependencyManagement>
    <dependencies>
        <!--当使用 Gradle 或 Maven 引用多个 JUnit 工件时，此物料清单 POM 可用于简化依赖项管理。不再需要在添加依赖时设置版本-->
        <dependency>
            <groupId>org.junit</groupId>
            <artifactId>junit-bom</artifactId>
            <version>${junit.jupiter.version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
<dependencies>
    <!--junit5-->
    <!-- 创建 Junit5 测试用例的 API-->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <!--对应添加的依赖的作用范围-->
        <scope>test</scope>
    </dependency>

    <!-- log日志 -->
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>${slf4j.version}</version>
        <scope>compile</scope>
    </dependency>
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>${logback.version}</version>
        <scope>compile</scope>
    </dependency>
</dependencies>

<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>${maven.compiler.version}</version>
            <configuration>
                <parameters>true</parameters>
                <!-- 设置jre版本为 17 -->
                <source>${java.version}</source>
                <target>${java.version}</target>
                <!-- 设置编码为 UTF-8 -->
                <encoding>${maven.compiler.encoding}</encoding>
            </configuration>
        </plugin>

        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>${maven-surefire-plugin.version}</version>
            <configuration>
            </configuration>
            <dependencies>
                <dependency>
                    <groupId>org.junit.jupiter</groupId>
                    <artifactId>junit-jupiter-engine</artifactId>
                    <version>${junit.jupiter.version}</version>
                </dependency>
                <dependency>
                    <groupId>org.junit.vintage</groupId>
                    <artifactId>junit-vintage-engine</artifactId>
                    <version>${junit.jupiter.version}</version>
                </dependency>
            </dependencies>
        </plugin>
    </plugins>
</build>
```

### 运行原理
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230104121305.png)

代码运行工具「IDE」运行`@Test`注解修饰的测试用例时通过`JUnit5`框架的`junit-jupiter`组件运行。


`@Test`注解其实就是告诉 `JUnit5` 框架需要运行哪些测试方法。

### 代码
`@Test`注解修饰的方法相当于声明的**测试用例**。

1. 编写类名一般以`Test`开头或结尾。
1. `@Test`注解导包为`org.junit.jupiter.api.Test`。
1. `@Test`注解修饰方法，放在方法上方。
1. `@Test`注解修饰的方法返回值类型为`void`。
1. `@Test`注解修饰的方法可直接运行。


### 示例
#### 初步编写
```java
import org.junit.jupiter.api.Test;

public class An_01Test_Test {
    @Test
    public void one(){
        System.out.println("第一个测试用例");
    }
}
```  
![](https://cdn.jsdelivr.net/gh/TesterDevSoul/pic/manual/20230104122217.png)

注意⚠️：
- 导包不要导错，不要导其他框架的`Test`包。

### 与Java的main()区别
- Class类中**方法个数不同**
  - Java中的`main()`方法在一个Class类中只能有**一**个
  - `@Test`注解修饰的方法在一个Class类中可以有**多**个
- Class类中**运行方式不同**
  - `main()`方法运行相当于直接运行类
  - 可以单独的运行每一个@Test注解修饰的方法，互不影响


 * 1. @Test注解修饰的方法可直接运行「@Test注解 是方法上的」
 * 2. 一个测试类里可以有多个@Test注解修饰的方法
 * 3. @Test注解作用类似Java代码中的main()方法入口
 * 4. @Test注解修饰的方法没有返回值，即方法声明时为void
 * 5. @Test注解里面编写的内容是测试用例执行的具体内容及断言结果






### junit 作为运行器

- 对应的代码库，有10个方法，每次都要运行，如果你可以用一种方法来写一个主方法，然后用钩子来调用所有这些方法
- `运行方法` --> `B()` --> `C()`

- 可以直接在运行方法上写`Test`注解进行运行

### 运行成功标志
- `Green Check`
![](https://gitee.com/datau001/picgo/raw/master/images/test/202112231510450.png)
- no news is good news
  - 没有消息就是好消息
- no failures means success
  - 没有失败就意味着成功


## 总结
- 总结一
- 总结二
- 总结三


[项目演示地址](https://github.com/TesterDevSoul/Tutorials/blob/master/junit5/junit5-basic/src/test/java/top/testeru/basic/An_01Test_Test.java)


