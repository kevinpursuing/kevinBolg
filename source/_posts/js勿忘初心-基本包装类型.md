---
title: 基本包装类型
date: 2017-10-16 16:40:25
tags: js-勿忘初心
categories: js之路
---

ECMAScript还提供了3个特殊的引用类型：Boolean,Number和String

```
var s1 = "some text";
var s2 = s1.substring(2);
```
过程：
1. 创建String类型的一个实例；
2. 在实例上调用制定的方法；
3. 销毁这个实例；

*引用类型与基本包装类型的主要区别就是对象的生存期。使用new操作符创建的引用类型的实例，在执行流离开当前作用域之前都一直保存在内存中。而自动创建的基本包装类型的对象，则只存在于一行代码的执行瞬间，然后立刻被销毁。这意味着我们不能在运行时为基本类型添加属性和方法。*

```
var s1 = "some text";
s1.color = "red";
alert(s1.color);   //undefined
```

### Boolean类型

### Number类型

```
var num = 10;
alert(num.toString());   //"10"
alert(num.toString(2));   //"1010"
alert(num.toString(8));   //"12"
alert(num.toString(10));   //"10"
alert(num.toString(16));   //"a"
```

*Number类型还提供了一些用于将数字格式化为字符串的方法*

**toFixed()方法会按照执行的小数位返回数值的字符串表示**

```
var num = 10;
alert(num.toFixed(2)) //10.00
```

如果数值本身包含的小数位比制定的还多，那么接近制定的最大小数位的值就会舍入，如下面的例子所示

```
var num = 10.005;
alert(num.toFixed(2));   //10.01
```


### String类型

String类型是字符串的对象包装类型

```
var stringObject = new String("hello world");
```

*字符方法*
两个用于访问字符串中特定祖父的方法是：chartAt()和charCodeAt()。这两个方法都接收一个参数，即基于0的字符位置。chartAt()方法以单字符字符串的形式返回给定位置的那个字符

```
var stringValue = "hello world";
alert(stringValue.charAt(1));   //"e"
```
如果你想得到的不是字符串而是字符编码，那么就要像下面这样使用charCodeAt()了


*字符串操作方法*
下面介绍与操作字符串有关的几个方法。第一个就是concat(),用于将一或多个字符串拼接起来，返回拼接得到的新字符串。

```
var stringValue = "hello" ;
var result = stringValue.concat("world");
alert(result);    //"hello world"
alert(stringValue)  //"hello"

var result1 = stringValue.concat("world","!");
alert(result1);  //"hello world!"
```

**虽然concat()是专门用来拼接字符串的方法，但实践中使用更多的还是加号操作符（+）。而且，使用几号操作符在大多数情况下都比使用concat()方法要简单易行（特别是在拼接多个字符串的情况下）**

、、、
var stringValue = "hello world";
alert(stringValue.slice(3));   //"lo world"
alert(stringValue.substring(3));   //"lo world"
alert(stringValue.substr(3));   //"lo world"
alert(stringValue.slice(3,7));   //"lo w"
alert(stringValue.substring(3,7));   //"lo w"
alert(stringValue.substr(3,7));   //"lo worl"


alert(stringValue.slice(-3));   //"rld"
alert(stringValue.substring(-3));   //"hello world"
alert(stringValue.substr(-3));   //"rld"
alert(stringValue.slice(3,-4));   //"lo w"
alert(stringValue.substring(3,-4));   //"hel"
alert(stringValue.substr(3,-4));   //""
、、、

*字符串位置方法*

```
var stringValue = "hello world";
alert(stringValue.indexOf("o"))   //4
alert(stringValue.lastIndexOf("o"))   //7
```

这两个方法都可以接收可选的第二个参数，表示从字符串中的哪个位置开始搜索

*trim()方法*
ECMAScript5为所有字符串定义了trim()方法。这个方法会创建以个字符串的副本，删除前置及后缀的所有空格，然后返回结果。

```
var stringValue = "  hello world  ";
var trimmedStringValue = stringValue.trim();
alert(stringValue);    //"  hello world  "
alert(trimmedStringValue);    //"hello world"
```
