# Spring 入门
## 课程目标
1. Spring 概述
2. Spring 使用场景
3. Spring 运行机制
4. Spring 执行流程

## Selenium Grid 概述
### 🤔Spring是什么

`Spring`是分层的Java SE/EE应用 `full-stack`(**全栈式**) **轻量级**开源框架

#### full-stack
全栈式：对各种主流技术和框架进行整合，同时对三层架构都提供了解决方案。

项目的三层架构为：`web`层、`service`层、`dao`层。
##### web层
- springmvc
##### service层
- spring的核心，进行事务的控制、对象的管理
##### dao层
- spring jdbc Template


#### 轻量级
轻量级、重量级的划分，依据为：
- 使用多少服务
- 启动时需要加载多少资源
- 项目耦合度

等等


提供了表现层 `SpringMVC` 和持久层 `Spring JDBC Template`以及 **业务层** 事务管理等众多的企业级应用 技术，还能整合开源世界众多著名的第三方框架和类库，逐渐成为使用最多的Java EE 企业应用开源框 架。
### 两大核心
以 **IOC**(`Inverse Of Control`:**控制反转**)和 **AOP**(`Aspect Oriented Programming`:**面向切面编程**)为内核。


## 总结
- Selenium Grid 概念
- Selenium Grid 使用场




1.2 Spring发展历程
 
* EJB
1997 年，IBM提出了EJB 的思想
1998 年，SUN制定开发标准规范 EJB1.0
1999 年，EJB1.1 发布
2001 年，EJB2.0 发布 2003 年，EJB2.1 发布 2006 年，EJB3.0 发布
* Spring
Rod Johnson( Spring 之父)
改变Java世界的大师级人物
2002年编著《Expert one on one J2EE design and development》 指出了JavaEE和EJB组件框架中的存在的一些主要缺陷;提出普通java类依赖注入更为简单的解
决方案。
2004年编著《Expert one-on-one J2EE Development without EJB》 阐述了JavaEE开发时不使用EJB的解决方式(Spring 雏形) 同年4月spring1.0诞生
1.3 Spring优势
  1)方便解耦，简化开发
Spring就是一个容器，可以将所有对象创建和关系维护交给Spring管理 什么是耦合度?对象之间的关系，通常说当一个模块(对象)更改时也需要更改其他模块(对象)，这就是
耦合，耦合度过高会使代码的维护成本增加。要尽量解耦
2)AOP编程的支持 Spring提供面向切面编程，方便实现程序进行权限拦截，运行监控等功能。
3)声明式事务的支持 通过配置完成事务的管理，无需手动编程
4)方便测试，降低JavaEE API的使用 Spring对Junit4支持，可以使用注解测试
5)方便集成各种优秀框架 不排除各种优秀的开源框架，内部提供了对各种优秀框架的直接支持
1.4 Spring体系结构
  2006年10月，发布 Spring2.0 2009年12月，发布 Spring3.0 2013年12月，发布 Spring4.0
2017年9月， 发布最新 Spring5.0 通用版(GA)
  
二 初识IOC 2.1 概述
控制反转(Inverse Of Control)不是什么技术，而是一种设计思想。它的目的是指导我们设计出更 加松耦合的程序。
控制:在java中指的是对象的控制权限(创建、销毁)
反转:指的是对象控制权由原来 由开发者在类中手动控制 反转到 由Spring容器控制 举个栗子
   * 传统方式
之前我们需要一个userDao实例，需要开发者自己手动创建 new UserDao();
* IOC方式 现在我们需要一个userDao实例，直接从spring的IOC容器获得，对象的创建权交给了spring控制
2.2 自定义IOC容器 2.2.1 介绍
需求
实现service层与dao层代码解耦合 步骤分析
1. 创建java项目，导入自定义IOC相关坐标 2. 编写Dao接口和实现类
2. 编写Service接口和实现类
3. 编写测试代码
2.2.2 实现 1)创建java项目，导入自定义IOC相关坐标
 <dependencies>
    <dependency>
        <groupId>dom4j</groupId>
        <artifactId>dom4j</artifactId>
        <version>1.6.1</version>
    </dependency>
    <dependency>
        <groupId>jaxen</groupId>
        <artifactId>jaxen</artifactId>
        <version>1.1.6</version>
    </dependency>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
  
2)编写Dao接口和实现类
public interface UserDao {
    public void save();
}
public class UserDaoImpl implements UserDao {
public void save() { System.out.println("保存成功了...");
} }
3)编写Service接口和实现类
public interface UserService {
    public void save();
}
public class UserServiceImpl implements UserService {
    private UserDao userDao;
    public void save(){
        userDao = new UserDaoImpl();
        userDao.save();
} }
4)编写测试代码
public class UserTest {
@Test
    public void testSave() throws Exception {
        UserService userService = new UserServiceImpl();
        userService.save();
} }