---
title: 引用类型-Function类型
date: 2017-10-05 14:01:33
tags: js-勿忘初心
categories: js之路
---

**说起来ECMAScript中什么最有意思，我想那莫过于函数了--而有意思的根源，则在于函数实际上是对象。每个函数都是Function类型的实例，而且都与其他引用类型一样具有属性和方法。由于函数是对象，因此函数实际上也是一个指向函数对象的指针，不会与某个函数绑定。函数通常是使用函数声明语法定义的，如下面的例子所示**

```
function sum(num1,num2) {
    return num1 + num2;
}
//这与下面使用函数表达式定义函数的方式相差无几
var sum = function(num1,num2){
    return num1 + num2;
};
```
最后一种定义函数的方式是使用Function构造函数。Function构造函数可以接收任意数量的参数，但最后一个参数始终都被看成式函数体，而前面的参数则枚举出了新函数的参数

*由于函数名仅仅式执行函数的指针，因此函数名与包含对象指针的额其他变量没有是呢嘛不同。换句话说，一个函数可能会有多个名字*

```
function sun(num1,num2){
    return num1 + num2;
}
alert(sum(10,10));  //20

var anotherSum = sum;
alert(anotherSum(10,10));  //20

sum = null;
alert(anotherSum(10,10));  //20
```

### 没有重载
将函数名想象为指针，也有助于理解为什么ECMAScript中没有函数重载的概念。

```
 function addSomeNumber(num) {
     return num + 100;
 }

 function addSomeNumber(num) {
     return num + 200;
 }

 var result - addSomeNumber(100); //300
```
显然，这个例子中声明了两个同名函数，而结果则是后面的函数覆盖了前面的函数。以上代码实际上与下面的代码没有什么区别。
```
var addSomeNumber = function (num){
    return num + 100;
}

addSomeNumber =function(num) {
    return num + 200;
}

var result = addSomeNumber(100) //300
```

*通过观察重写之后的代码，很容易看清楚到底是怎么回事儿--在创建第二个函数时，实际上覆盖了引用第一个函数的变量addSomeNumber*

### 函数声明与函数表达式

本节到目前为止，我们一直没有对函数声明和函数表达式加以区别。而实际上，解析器在向执行环境中加载数据时，对函数声明核函数表达式并非一视同仁。解析器会率先读取函数声明，并使其在执行任何代码之前可用（可以访问）；至于函数表达式，则必须等到解析器执行到它所在的代码行，才会真正被解释执行

### 作为值得函数
因为ECMAScript中的函数名本身就是变量，所以函数也可以作为值来使用。也就是说，不仅可以像传递参数一样把一个函数传递给另一个函数，而且可以将一个函数作为另一个函数的结果返回。
```
function callSomeFunction(someFunction,someArgument) {
    return someFunction(someArgument);
}

function add10(num){
    return num + 10;
}
var result = callSomeFunction(add10,10);
alert(result1);  //20
```

**当然，可以从一个函数中返回另一个函数，而且这也是极为有用的一种技术。例如，假设有一个对象数组，我们想要根据某个对象属性对数组进行排序。而传递给数组sort()方法的比较函数要接受两个参数，即要比较的值。可是，我们需要一种方式来知名按照哪个属性来排序。要解决这个问题，可以定义一个函数，它接收一个属性名，然后根据这个属性名来创建一个比较函数**

```
 function createComparisonFunction(propertyName) {
     return function(object1,object2) {
         var value1 = object[propertyName];
         var value2 = object[propertyName];
         if (value1 < value2){
             return -1;
         }else if(value1 > value2){
             return 1;
         } else {
             return 0;
         }
     }
 }

 var data = [{name:"Zachary",age:28},{name:"Nicholas",age:29}];

 data.sort(createComparisionFunction("name"));
 alert(data[0].name); //Nicholas
 
 data.sort(createComparisonFunction("age"));
 alert(data[0].name); //Zachary
```


### 函数内部属性

在函数内部，有两个特殊的对象：arguments和this。arguments是一个类数组对象，包含着传入函数中的所有参数。虽然arguments的主要用途是保存函数参数，但这个对象还有一个名叫callee的属性，该属性是一个指针，指向拥有这个arguments对象的函数。请看下面这个非常经典的阶乘函数。

```
function factorial(num){
    if(num<=1){
        return 1;
    }else{
        return num * factorial(num-1)
    }
}
```
定义阶乘函数一般都要用到递归算法；如上面的代码所示，在函数有名字，而且名字以后也不会变得情况下，这样定义没有问题。但问题是这个函数的执行与函数名factorial紧紧耦合在了一起。为了消除这种紧密耦合的现象。可以想下面这样使用arguments.callee.

```
function factorial(num) {
    return 1;
}else{
    return num * arguments.callee(num-1)
}
```

*在这个重写后的factorial()函数的函数体内，没有在引用函数名factorial。这样，无论引用函数式使用的是什么名字，都可以保证正常完成递归调用*

```
var trueFactorial = factorial;
factorial = function(){
    return 0;
}
alert(trueFactorial(5));  //120
alert(factorial(5));   //0
```

