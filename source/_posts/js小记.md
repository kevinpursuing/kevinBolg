---
title: js小记
date: 2017-09-27 15:39:31
tags: js之路
---

> 三座大山
 * 原型 原型链
 * 作用域 闭包
 * 异步 单线程

 # 基础

 ## 变量的类型和计算
   ### typeof(用来判断变量的类型)
   undefined -> undefined

   '123' -> string

   123 -> number

   true -> boolean

   [] -> object

   {} -> object

   consolo.log -> function

   **(typeof只能区分出值类型，引用类型可以区分出函数)**

  > 那什么是值类型？什么是引用类型呢，看一段代码
    
**值类型**

 ```
 var a = 100;
 var b = a;
 a = 20;
 console.log(b) //100
```

**引用类型**

   ```
   var a = {age:20}
   var b =a
   b.age = 21
   console.log(a.age)  //21
   ```

**对象，数组，函数（为了省内存）**
