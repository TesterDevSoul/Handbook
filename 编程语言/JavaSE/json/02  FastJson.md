#  FastJson
## 课程目标
1.  JSON 概述
2.  JSON 特点
3.  XML与JSON的区别

## JSON语法格式


JSON数据示例：

```
{
	"id": 01,
	"name": "美少女战士",
	"age": 18
}
```

### 语法规范 

1. 数据最外层由`{}`括起来

2. 数据以`"键:值"`对的形式出现
>其中**键**多以**字符串**形式出现<br/>
>**值**可取**字符串**，**数值**，甚至其它**json对象**
3. 每两个`"键:值"`对中间以英文逗号`,`分隔
>最后一个"键：值"对省略逗号
4. 参数值如果是`string`类型，就**必须加引号**
5. 参数值如果是**数字**类型，**引号可加可不加**

遵守上面几点，便是一个json对象的规范。



代码示例: 

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<script typet="text/javascript" src="http://libs.baidu.com/jquery/1.9.1/jquery.min.js"></script>

    <script>

        //自定义JSON数据格式 (Java中的对象)
        var person = {"name":"tom","sex":"女", "age":12};
        console.log(person);

        //数组格式
        var persons = {"person":[{"name":"tom","sex":"女", "age":12},{"name":"jack","sex":"男", "age":22}]};
        console.log(persons);

        //集合
        var list = [{"name":"老五","sex":"女", "age":12},{"name":"会长","sex":"男", "age":12}];
        console.log(list);

    </script>
</head>
<body>

</body>
</html>
```




    
## 总结
- Selenium Grid 概念
- Selenium Grid 使用场

