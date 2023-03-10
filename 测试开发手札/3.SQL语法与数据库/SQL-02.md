---
theme: "league"
transition: "fade"
title: "霍格沃兹测试开发"
use: hogwarts
---

# MySQL

霍格沃兹测试开发学社

ceshiren.com


---


## 目录

- DML操作表中数据
- DQL查询表中数据


---

## DML操作表中数据

DML 用于对表中的数据进行**增**、**删**、**改**操作。



---



## 插入数据

- 命令模版：「见右侧🫱」
  - 方式1：插入全部字段， 将所有字段名都写出来。
  - 方式2：插入全部字段，不写字段名。
  - 方式3：插入指定字段的值。
  
```sql
insert into 表名 (字段名1，字段名2...) values(字段值1，字段值2...);
```



---



### 准备: 创建学生表

- 表名:student 
- 表中字段:
  - 学员ID：sid int
  - 姓名：sname varchar(20) 
  - 年龄：age int
  - 性别：sex char(1)
  - 地址：address varchar(40)


---




### 需求: 插入全部字段


- 插入数据为：
  - 学员ID：1
  - 姓名：孙悟空
  - 年龄：20
  - 性别：男
  - 地址：花果山


---



### 需求: 不写字段名插入字段


- 插入数据为：
  - 学员ID：2
  - 姓名：孙悟饭
  - 年龄：10
  - 性别：男
  - 地址：地球


---




### 需求: 插入指定字段的值

- 插入数据为：
  - 姓名：白骨精




---


### 注意

1. 值与字段必须要对应，**个数相同** & **数据类型**相同。 

1. 值的数据大小，必须在字段指定的长度范围内。

1. `varchar` `char` `date`类型的值必须使用单引号，或者双引号 包裹。 

1. 如果要插入空值，可以忽略不写，或者插入`null`。

1. 如果插入指定字段的值，必须要上写列名。


---

## 更改数据 

- 不带条件的修改
- 带条件的修改

---


### 不带条件的修改

- 命令模版：「见右侧🫱」


```sql
update 表名 set 列名 = 值
```

---



### 带条件的修改

- 命令模版：「见右侧🫱」

```sql
update 表名 set 列名 = 值 [where 条件表达式:字段名 = 值 ]
```



---



### 需求: 不带条件修改

- 将所有的性别改为女。「慎用」




---




### 需求: 带条件的修改

- 将sid为 5 的学生，性别改为 男。



---



### 需求: 一次修改多个列

-  将sid为 2 的学员，年龄改为 20，地址改为 北京。



---


## 删除数据 

- 删除所有数据
- 指定条件删除数据



---





### 删除所有数据

- 命令模版：「见右侧🫱」
- 需求2: 
  - 删除student表中所有数据。

```sql
delete from 表名
```



---





### 指定条件删除数据

- 命令模版：「见右侧🫱」
- 需求1: 
  - 删除student表中 sid 为 1 的数据。

```sql
delete from 表名 [where 字段名 = 值]
```



---


### 删除表所有数据

有两种做法：

1. `delete from 表名`。
  
2. `truncate table 表名`。「推荐」



---

##  DQL 查询表中数据 

- 数据准备：

  - 创建表。

  - 插入数据。


---

### 创建表

代码准备，创建员工表:

- 表名:emp。 
- 表中字段:
  - 员工ID：eid int。
  - 姓名：ename varchar(20) 。
  - 性别：sex char(1)。
  - 薪资：salary double。
  - 入职时间：hire_date date。
  - 部门名称：dept_name varchar(10)。


---

### 插入数据
- 1,孙悟空,男,7200,2013-02-04,教学部。
- 2,猪八戒,男,3600,2010-12-02,教学部。
- 3,唐僧,男,9000,2008-08-08,教学部。
- 4,白骨精,女,5000,2015-10-07,市场部。
- 5,蜘蛛精,女,5000,2011-03-14,市场部。
- 6,玉兔精,女,200,2000-03-14,市场部。
- 7,林黛玉,女,10000,2019-10-07,财务部。
- 8,黄蓉,女,3500,2011-09-14,财务部。
- 9,吴承恩,男,20000,2000-03-14,NULL。
- 10,孙悟饭,男, 10,2020-03-14,财务部。
- 11,兔八哥,女, 300,2010-03-14,财务部。




---

## 查询

- 查询包括：**简单查询**和**条件查询**。

- 关键字为： **SELECT**。



---


## 简单查询

- 命令模版：「见右侧🫱」



```sql
select 列名 from 表名
```



---




### 需求: 查询所有数据


查询emp中的所有数据。




---




### 需求: 查询部分列

查询emp表中的所有记录，仅显示id和name字段。



---



### 需求: 别名查询

- 别名查询，使用关键字：**as**。

- 将所有的员工信息查询出来，并将列名改为中文。 
  - eid ：编号
  - ename ：姓名
  - sex ：性别
  - salary ：薪资
  - hire_date：入职时间
  - dept_name：部门名称



---



### 需求: 去重查询

- 去重查询，使用去重关键字：**DISTINCT**。

- 查询员工表中一共有几个部门。




---


### 需求: 运算查询

- 运算查询 (查询结果直接参与运算)。

- 将所有员工的工资 +3000 元进行显示。


---



## 条件查询 

- 先取出表中的每条数据，满足条件的数据就返回，不满足的就过滤掉。

- 命令模版：「见右侧🫱」

```sql
select 列名 from 表名 where 条件表达式
```


---



### 运算符

1. 比较运算符
2. 逻辑运算符


---



### 1. 比较运算符

|运算符|说明|
|---|---|
|`> < >= <= = <> !=`|大于、小于、大于等于、小于等于、等于、不等于 |
|`BETWEEN ...AND...`|显示在某一区间的值|
|`IN(集合)`| 集合表示多个值,使用逗号分隔|
|`LIKE '%张%'`|模糊查询|
|`IS NULL`|查询某一列为NULL的值,注:不能写 `= NULL`|


---


### 2.逻辑运算符
   
|运算符|说明|
|---|---|
|`And &&`|多个条件同时成立。|
|`Or \|\|`|多个条件任一成立。|
|`Not`| 不成立，取反。|



---



### 需求

1. 查询员工**姓名**为**黄蓉**的员工信息。

2. 查询**薪水**价格为**5000**的员工信息。

3. 查询**薪水**价格**不是5000**的所有员工信息。

4. 查询**薪水**价格**大于6000**元的所有员工信息。

5. 查询**薪水**价格**在5000到10000之间**所有员工信息。

6. 查询**薪水**价格**是3600或7200或者20000**的所有员工信息。





---



### 需求

|通配符 |说明|
|--- |---|
|% |表示匹配任意 **多个** 字符串 |
|_ |表示匹配 **一个** 字符|

1. 查询**含有**'**精**'字的所有员工信息。

2. 查询以'**孙**'**开头**的所有员工信息。

3. 查询第**二**个字为'**兔**'的所有员工信息。

4. 查询**没有部门**的员工信息。

5. 查询**有部门**的员工信息。





---




## 查询总结


```sql
-- 查询表中的所有数据
SELECT * FROM table_name;

-- 查询表中指定的列
-- “column1”和“column2”是要查询的列名。
SELECT column1, column2 FROM table_name;

-- 查询满足指定条件的行
-- “condition”是查询条件，例如“age > 18”表示查询年龄大于18岁的行。
SELECT * FROM table_name WHERE condition;

-- 对查询结果进行排序
-- “column_name”是要排序的列名，[ASC|DESC]表示升序或降序排列。
SELECT * FROM table_name ORDER BY column_name [ASC|DESC];


-- 对查询结果进行分组和聚合计算
-- “column1”是要分组的列名，
-- aggregate_function可以是SUM、AVG、COUNT等聚合函数，
-- 用于对指定列进行计算。
SELECT column1, aggregate_function(column2) FROM table_name GROUP BY column1;

-- 查询满足多个条件的行
-- “condition1”和“condition2”是查询条件，AND表示同时满足两个条件。
SELECT * FROM table_name WHERE condition1 AND condition2;

```



---




## DQL操作单表

- 排序
- 聚合函数
- 分组
- 分页


---



## 排序

- `ORDER BY`：排序只是显示效果,不会影响真实数据。

- 命令模版：「见右侧🫱」
  
  - ASC：表示升序排序(默认) 。
  
  - DESC：表示降序排序。
  
- 排序方式：单列排序、组合排序


```sql
SELECT 字段名 FROM 表名 [WHERE 字段 = 值] ORDER BY 字段名 [ASC / DESC]
```




---



### 需求：单列排序

- 使用 **salary** 字段,对emp表数据进行升序排序。

- 使用 **salary** 字段,对emp表数据进行降序排序。






---


### 需求：组合排序


在**薪水**降序排序的基础上,再使用**id**进行排序, 如果薪水相同就以id做**降序**排序。





---



##  聚合函数 

- **纵向查询**
- **对某一列的值进行计算**。

- 命令模版：「见右侧🫱」



```sql
SELECT 聚合函数(字段名) FROM 表名;
```


---




### 常用的聚合函数


|聚合函数|作用|
|---|---|
|`count`(字段)|统计列**不为NULL**的行数| 
|`sum`(字段) |计算指定列的数值**和**|
|`max`(字段) |计算指定列的最**大**值|
|`min`(字段) |计算指定列的最**小**值|
|`avg`(字段) |计算指定列的**平均**值|


---


### SUM函数

- 用于对某一列的数值进行求和计算。基本语法：
- 需求：
  - 订单表orders，其中包含订单编号order_id和订单金额amount两个列。
  - 使用SQL查询语句对订单金额进行求和计算。

```sql
-- column_name是要进行求和计算的列名。
SELECT SUM(column_name) FROM table_name;
```










---



### AVG函数
- 用于对某一列的数值进行平均值计算。基本语法：
- 需求：
  - 学生表students，其中包含学生姓名name、学生年龄age和学生成绩score三个列。
  - SQL查询语句对学生成绩进行平均值计算。
  
```sql
-- column_name是要进行平均值计算的列名。
SELECT AVG(column_name) FROM table_name;
```

---




### COUNT函数
- 用于对某一列的数据进行计数操作。基本语法：
- 需求：
  - 学生表students，其中包含学生姓名name、学生年龄age和学生成绩score三个。
  - 查询语句对学生数量进行计数。




```sql
-- column_name是要进行计数操作的列名。
SELECT COUNT(column_name) FROM table_name;
```


---



### MIN函数和MAX函数
- MIN函数用于对某一列的数据进行最小值计算。
- MAX函数用于对某一列的数据进行最大值计算。
- 基本语法：
- 需求：
  - 订单表orders，其中包含订单编号order_id和订单金额amount两个列。
  - 查询语句对订单金额进行最小值和最大值计算。


```sql
-- column_name是要进行最小值或最大值计算的列名。
SELECT MIN(column_name) FROM table_name;
SELECT MAX(column_name) FROM table_name;
```


---



### 需求

1. 查询员工的总数。
2. 查看员工总薪水、最高薪水、最小薪水、薪水的平均值。
3. 查询薪水大于4000员工的个数。
4. 查询部门为'教学部'的所有员工的个数。
5. 查询部门为'市场部'所有员工的平均薪水，显示为：市场部平均薪资。



---



## 分组

- **GROUP BY**：对查询的信息进行分组，相同数据作为一组。


- 命令模版：「见右侧🫱」
- 需求：
  - 学生成绩表scores，其中包含姓名name、科目subject和成绩score三列。- 科目对成绩进行分组，并且分别计算成绩平均值、成绩总和。


```sql
SELECT column1, column2, aggregate_function(column3)
FROM table_name
WHERE condition
GROUP BY column1, column2;
```


---



### 需求

通过**性别字段**进行分组，求各组的平均薪资。


---


### 需求

1. 查询emp有几个部门。

2. 查询emp每个部门的平均薪资。
   
3. 查询emp每个部门的平均薪资, 部门名称不能为null。

4. 查询平均薪资大于6000的部门，部门名称不能为null。



---



## limit关键字 



- 命令模版：「见右侧🫱」
- 需求：
  - 学生表students，其中包含学生姓名name、学生年龄age和学生成绩score三个列。
  - 使用SQL查询语句获取前10个学生的信息。
  - 使用SQL查询语句获取第11到第20个学生的信息。


```sql
-- offset 起始行数, 从0开始记数, 如果省略 则默认为 0.
-- count 返回的行数
SELECT 字段1,字段2... FROM 表名 LIMIT offset , count;
```



---


### 需求

1. 查询emp表中的前 5条数据。
2. 查询emp表中从第4条开始,查询6条。



---



### 需求: 分页操作 

每页显示3条数据，第一页SQL，第二页SQL，第三页SQL语句分别如何写？


