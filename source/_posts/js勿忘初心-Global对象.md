---
title: Global对象和Math对象
date: 2017-10-20 16:40:25
tags: js-勿忘初心
categories: js之路
---

Global（全局）对象可以说是ECMAScript中最特别的一个对象了，因为不管你从什么角度上看，这个对象都是不存在的。ECMAScript中的Global对象在某种意义上是作为一个终极的“兜底儿对象”来定义的。换句话说，不属于任何其他对象的属性和方法，最终都是它的属性和方法。事实上，没有全局变量或全局函数；所有在全局作用域中定义的属性和函数，都是Global对象的属性。本书前面介绍过的那些函数，诸如isNaN(),isFinite(),parseInt()以及parseFloat(),实际上全都是Global对象的方法。除此之外，Global对象还包含其他的一些方法。

**URL编码方法**
Global对象的encodeURI()和encodeURIComponent()方法可以对URI(Uniform Resource Identifiers,通用资源标识符)进行编码，以便发给浏览器。有效的URI中不能包含某些自负，例如空格。他们的主要区别在于，encodeURI()不会对本身属于URI的特殊字符进行编码，例如冒号，政协刚，问好和井号；而encodeURIComponent()则会对它发现的任何非标准字符进行编码

**一般来说，我们使用encodeURIComponent()方法的时候要比使用encodeURL()更多，因为在实践中更常见的是对查询字符串使用encodeURIComponent()的原因所在**

**eval()方法**
现在，我们介绍最后一个--大概也是整个ECMAScript语言中最强大的一个方法：eval()。eval()方法就像是一个完整的ECMAScript解析器，它只接受一个参数，即要执行的ECMAScript（或 JavaScript）字符串

```
eval("alert('hi')");

// 这行代码的作用等价于下面这行代码：

alert("hi");
```

*通过eval()执行的代码被认为是包含盖茨调用的执行环境的一部分，因此被执行的代码具有与该执行环境相同的作用域链。这意味着通过eval()执行的代码可以引用在包含环境中东一的比变量*

```
var msg = "hello world";
eval("alert(msg)");   //"hello world"
```

**能够解释代码字符串的能力非常强大，但也非常危险。因此在使用eval()时必须极为谨慎，特别是在用它执行用户输入数据的情况下。否则，可能会有恶意用户输入威胁你的站点或应用程序安全的代码（即所谓的代码注入）**

Global对象的所有属性：
1. 特殊值
* undefined
* NaN
* Infinity

2. 构造函数
* Object    
* Array
* Function
* Boolean
* String
* Number
* Date
* RegExp
* Error
* EvalError
* RangeError
* ReferenceError
* SyntaxError
* TypeError
* URIError

*ECMAScript 5明确禁止给undefined,NaN和Infinity赋值，这样做即使在非严格模式下也会导致错误*

### window对象
ECMAScript虽然没有指出如何直接访问Global对象，但Web浏览器都是将这个全局对象作为window对象的一部分加以实现的。因此，在全局作用域中声明的所有变量和函数，这都成了window对象的属性


## Math对象

ECMAScript还为保存数学公式和信息提供了一个公共位置，即Math对象。与我们在JavaScript直接编写的计算功能相比，Math对象提供的计算功能执行起来要快得多。Math对象中还提供了辅助完成这些计算的属性和方法

**min()和max()方法**
min()方法和max()方法用于确定一组数值中的最小值和最大值。这两个方法都可以接收任意多个数值参数

```
var max = Math.max(3,54,32,16)
alert(max);   //54

var min = Math.min(3,54,32,16)
alert(min);   //3 
```

*要找到数组中的最大或最小值，可以像下面这样使用apply()方法*

```
var values = [1,2,3,4,5,6,7,8];
var max = Math.max.apply(Math,values);
```

**舍入方法**
Math.ceil()执行向上舍入：即它总是将数值向上舍入为最接近的整数;
Math.floor()执行向下舍入：即它总是将数值向下舍入为最接近的整数;
Math.round()执行标准舍入：即它总是将数值四舍五入为最接近的整数;

**random()方法**
Math.random()方法返回大于等于0小于1的一个随机数