---
title: 面向对象的程序设计
date: 2017-10-21 13:22:25
tags: js-勿忘初心
categories: js之路
---

**面思想对象的语言有一个标志，那就是它们都有类的概念，而通过类可以创建任意多个相同属性和方法的对象。ECMAScript中没有类的概念，因此它的对象也与基于类的语言中的对象有所不同**

ECMA-262把对象定义为：“无序属性的集合，其属性可以包含基本值，对象或者函数。”严格来讲，这就相当于说对象是一组没有特定顺序的值。对象的每个属性或方法都有一个名字，而每个名字都映射到一个值。正因为这样，我们可以吧ECMAScript的对象想象成散列表；无非就是一组名值对，气其中值可以使数据或函数


### 理解对象
创建自定义对象最简单方式就是创建一个Object的实例，然后再为它添加属性和方法

```
var person = new Object();
persion.name = "Kevin";
person.age = 29;
person.job = "Web Engineer";

person.sayname = function(){
    alert(this.name);
}
```
*几年后，对象字面量成为创建这种对象的首选模式*

```
var person = {
    name: "Kevin",
    age: 24,
    job: "Web Engineer",
    sayName: function(){
        alert(this.name);
    }
};
```

### 属性类型*

**1. 数据属性**

数据属性包含一个数据值的位置。在这个位置可以读取和写入值。数据属性有4个描述其行为的特性

1. Configurable: 表示能否通过delete删除属性从而重新定义属性，能否修改属性的特征，或者能否把属性修改为访问器属性。默认值为true

2. Enumerable: 表示能否通过for-in循环返回属性。默认值为true

3. Writable: 表示能否修改属性的值。默认值为true

4. Value: 包含这个属性的数据值。默认值为undefined

*要修改属性默认的特性，必须使用ECMAScript5的Object.defineProperty()方法。这个方法接收三个函数：属性所在的对象，属性的名字和一个描述符对象。描述符对象的属性必须是以上4个属性中的一个或多个*

```
var person = {};
Object.defineProperty(person,"name",{
    writable:false,
    value:"Kevin"
})

alert(person.name);  //Kevin
person.name = "Greg";
alert(person.name);  //Kevin
```

**访问器属性**
访问器属性不包含数据值：他们包含一对儿getter和setter函数（不过，这两个函数不是必需的）。在读取访问器属性时，会调用getter函数，这个函数负责返回有效的值；在写入访问器属性时，会调用setter函数并传入新值，这个函数负责决定如何处理数据。访问器属性有如下4个特性。

1. Configurable: 表示能否通过delete删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为数据属性。默认值为true

2. Enumerable: 表示能否通过for-in循环返回属性。对于直接在对象上定义的属性。默认值为undefined

3. Get: 在读取属性时调用的函数。默认值为undefined

4. Set: 在写入属性时调用的桉树。默认值为undefined

*访问器不能直接定义，必须使用Object.defineProperty()来定义*

```
var book= {
    _year:2004,
    edition: 1
}

Object.defineProperty(book,"year",{
    get: function(){
      return this._year;
    },
    set: function(newValue){
        if(newValue > 2004){
            this._year = newValue;
            this.edition += newValue - 2004;
        }
    }
})

book.year = 2005;
alert(book.edition);   //2
```

*这是使用访问器属性的常见方法，即设置一个属性的值会导致其他属性发生变化*


### 定义多个属性

由于为对象定义多个属性的可能性很大，ECMAScript 5又定义了一个Object.defineProperties()方法。

```
var book = {}

Object.defineProperties(books,{
    _year: {
        value: 2004
    },

    edition: {
        value: 1
    },

    year: {
        get: function(){
           return this._year;
        },

        set: function(){
           if (newValue > 2004) {
               this._year = newValue;
               this.edition += newValue - 2004;
           }
        }
    }
});
```

### 读取属性的特性

使用ECMAScript 5的Object.getOwnPropertyDescriptor()方法，可以取得给定属性的描述符

