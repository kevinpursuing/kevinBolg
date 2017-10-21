---
title: js中的this以及函数的属性和方法
date: 2017-10-16 15:01:33
tags: js-勿忘初心
categories: js之路
---

**函数内部的另一个特殊对象是this，其行为与java和c##中的this大致类似，this引用的是函数据以执行的环境对象--或者也可以说是this值（档子网页的全局作用域中调用函数时，this对象引用的就是window）**

```
window.color="red";
var o = {color:"blue"};

function sayColor(){
    alert(this.color);
}

sayColor();  //"red"

o.sayColor = sayColor();
o.sayColor();   //"blue"
```

*注意：函数的名字仅仅是一个包含指针的变量而已，因此，即使是在不同的环境中执行，全局的sayColor()函数与o.sayColor()只想的仍然是同一个函数*

ECMAScript5也规范化了另一个函数对象的属性：caller。这个属性保持着电泳当前函数的函数的引用，如果实在全局作用域找那个调用当前函数，它的值为null。例如：

```
function outer() {
    inner();
}

function inner(){
    alert(inner.caller);
}

outer();
```

*以上代码会导致警告矿中的显示out()函数的源代码。因为outer()调用了inter(),所以inner.caller就指向outer()。为了实现更松散的耦合，也可以通过arguments.callee.caller来访问相同的信息*


## 函数的属性和方法

ECMAScript中的函数是对象，因此函数也有属性和方法。每个函数都包含两个属性：length和prototype。其中，length属性表示函数希望接收的命名参数的个数

**在ECMAScript核心所定义的全部属性中，最耐人寻味的就要数prototype属性了。对于ECMAScrip中的引用类型而言，prototype是保存他们所有实例方法真正所在。换句话说，诸如toString()和valueOf()等方法实际上都保存在prototype名下，只不过是通过各自对象的实例访问罢了。在EMAScript5中，prototype属性是不可枚举的，因此使用for-in无法发现**

每个函数都包含两个非继承而来的方法：apply()和call()。这两个方法的用途都是在特定的作用域中调用函数，实际上等于设置函数体内this对象的值。首先，apply()方法接收两个参数：一个是在其中运行函数的作用域，另一个是参数数组。其中，第二个参数可以使Array的实例，也可以是arguments对象。
call()方法与apply()方法的作用相同，他们的区别仅在与接收参数的方式不同。对于call()方法而言，第一个参数是this值没有变化，变化的是其余参数都直接传递给函数。欢聚话说，在使用call方法时，传递给函数的参数必须逐个列举出来。

*事实上，传递参数并非apply()和call()真正地用武之地；他们真正强大的地方是能够扩充函数赖以运行的作用域*

```
window.color = "red";
var o = {color: "blue" };
function sayColor(){
    alert(this.color);
}

sayColor();    //red

sayColor.call(this);    //red
sayColor.call(window);   //red
sayColor.call(o);   //blue
```

*使用call()来扩充作用域的最大好处，就是对象不需要与方法有任何耦合关系*

ECMAScript 5还定义了一个方法：bing()。这个方法会创建一个函数的实例，其this值会被绑定到传给bind()函数的值。
*bing()会返回一个修改之后的函数*
```
window.color = "red";

var o = {color:"blue"};

function sayColor(){
    alert(this.color);
}

var objectSayColor = sayColor.bind(o);
objectSayColor();  //blue
```