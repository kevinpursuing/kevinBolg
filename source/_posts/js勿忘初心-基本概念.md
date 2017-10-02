---
title: 基本概念
date: 2017-10-02 13:49:30
tags: js-勿忘初心
---

### 语法

ECMAScript的语法大量借鉴了C及其类C语言的语法

**区分大小写**

要理解的第一个概念就是ECMAScript中的一切都区分大小写，，这也就意味着，变量名test和变量名Test分别表示两个不同的变量，而函数名不能使用typeof，因为它是一个关键字，但typeof则完全可以是一个有效的函数名。

**标识符**

所谓标识符，就是指变量，函数，属性的名字，或者函数的参数。标识符可以使按照下列各式规则组合起来的一或多个字符：
 * 第一个字符必须是一个字母，下划线（_）,或一个美元符号（$）
 * 其他字符可以使字母，下划线，美元符号或数字
 按照惯例，ECMAScript标识符采用驼峰式大小写格式，也就是第一个字母小写，剩下的每一个单词的首字母大写

 没有谁强制要求必须采用这种格式，但为了与ECMAScript内置的函数和对象命名格式保持你一致，可以将其当做一种最佳实践

 **注释**
```
  // 单行注释

  /*
   * 这是一个多行
   *（块级）注释
   */
```
ECMAScript
**严格模式**

ECMAScript5 引入了严格模式的概念，严格模式是为JavaScript定义了一种不同的解析与执行模型。在严格模式下，ECMAScript3中的一些不确定的行为将得到处理，而且对某些不安全的操作也会抛出错误。要在整个脚本中启用严格模式，可以再顶部添加如下代码：
``` 
 use strict 
```

**语句**

ECMAScript中的语句以一个分号结尾；如果省略分号，则由解析器确定语句的结尾

*虽然语句结尾的分号不是必须的，但我们建议任何时候都不要省略它，因为加上这个分号可以避免很多错误，开发人员也可以放心的通过删除多余的空格来压缩ECMAScript代码*

虽然条件控制语句（如if语句）只在执行对跳语句的情况下才要求使用代码块，但最佳时间是始终在控制语句中使用代码块-即使代码块中只有一条语句

在控制语句中使用的代码块可以让编码意图更加清晰，而且也能降低修改代码是出错的几率


## 关键字和保留字

ECMAScript的全部关键字
  break do instanceof typeof case else new var catch
  finally return void continue for switch while debugger 
  function this with default if throw delete in try

ECMA-262第3版定义的全部保留字
  abstract enum init short boolean export interface static byte extends long super char final native synchronized class float package throws const goto private transient debugger implement protected volatile double import public
*以上只是第三版的，仅供参考*

## 变量
  ECMAScript的变量是宋丹类型的，所谓松散类型就是可以用来保存任何类型的数据。换句话说，每个变量仅仅是一个用于保存至的占位符而已

  不建议修改变量所保存值得类型，但这种操作在ECMAScript中完全有效

## 数据类型
  基本数据类型：Undefined,Null,Boolean,Number,String
  复杂数据类型：Object。Object本质上是由一组无序的名值对组成的

  **typeof操作符**
  鉴于ECMAScript是松散类型的，因此需要有一种手段来检测给定变量的数据类型
   “undefined”--如果这个值未定义
   “boolean”--如果这个值是布尔值
   “string”--如果这个值是字符串
   “number”--如果这个值是数值
   “object”--如何这个值是对象或者nul
   “function”--如果这个值是函数

   *从技术角度讲，函数在ECMAScript中是对象，不是一种数据类型，然而，函数也确实有一些特殊的属性，因此通过typeof操作符来区分函数和其他对象是有必要的*

   **Undefined类型**

   Undefined类型只有一个值，即特殊的undefined.在使用var声明变量但未对其加以初始化时，这个变量的值就是undefined

   **Null**
   Null类型是第二个只有一个值的数据类型，这个特殊的值是null。从逻辑角度来看，null值表示一个空对象指针，而这也是使用typeof操作符检测null值时会返回object的原因

   **Boolean类型**
   Boolean类型是ECMAscript中使用得最多的一种类型，该类型只有两个字面值：true和false

   **Number类型**

   由于保存浮点数值需要的内存空间是保存整数值得两倍，因此ECMAScript会不失时机地将浮点数值转换为整数值，如何小数点后面没有跟任何数字，那么这个数值就可以作为整数值来保存，同样地，如果浮点数值本身表示的就是一个整数（如1.0），那么该值也会被转换为整数。

   如果两个数是0.1和0.2，那么测试将无法通过，因此，永远不要测试某个特定的浮点数值

   *关于浮点数值计算会产生摄入误差的问题，有一点需要明确；这是使用基于IEEE754数值的浮点计算的通病，ECMAScript并非独此一家；其他使用相同数值格式的语言也存在这个问题*

   *NaN*
   NaN,即非数值，是一个特殊的数值，这个数值勇于表示一个本来要返回数值的操作数未返回数值的情况

   NaN有两个非同寻常的特点：首先，任何涉及NaN的操作（例如NaN/10）都会返回NaN,这个特点在多步计算中有可能导致为题。其次，NaN与任何值都不相等，包括NaN本身

   针对NaN的这两个特点，ECMAScript定义了isNaN()函数。这个函数接收一个参数，该参数可以是任何类型，而函数会帮我们确定这个参数是否“不是数值”。isNaN()在接收带一个值之后，会尝试将这个值转换为数值。某些不是数值的值会直接转换为数值，例如字符串“10”或Blooean值。而任何不能被转化为数值的值都会导致这个函数返回true。

   *数值转换*
   有3个函数可以把非数值转换为数值：Number(),parseInt(),parseFloat()

   parseInt()会忽略字符串前面的空格，制止找到第一个非空格字符。如果第一个字符不是数字字符或者负号，parsrInt()就是返回NaN;如果第一个字符是数字字符，它会继续解析第二个字符，知道解析完所有后续字符或者遇到了一个非数字字符

   与parseInt()函数类似，parseFloat()也是从第一个字符开始解析每个字符。而且也是一直解析到字符串末尾，或者解析到遇见一个无效的浮点数字字符为止。也就是说，字符串中的第一个小数是有效的，而第二个小数点就是无效的了，因此他后面的字符串将被忽略

   **String类型**
   String类型用户表示由零或多个16位Unicode字符组成的字符序列，即字符串。字符串可以由双引号或单引号表示

   *转换为字符串*
```
var age = 11;
var ageAsString = age.toString();
```
还有一种方法，就是可以使用加号操作符把它与一个字符串加在一起





## Object类型

ECMAScript中的对象其实就是一组数据和功能的集合。对象可以通过执行new操作符后跟要创建的对象类型的名称来创建。而创建Object类型的实力并为其添加属性或方法，就可以创建自定义对象

    var o =new Object();

仅仅创建Object的实力并没有什么用处，但关键是要理解一个重要的思想：即在ECMAScript中，Object是所有它的实例的基础。换句话说，Object类型所具有的任何属性和方法也同样存在于更具体的对象中

  Object的每个实例都具有下列属性和方法
  * constructor:保存着用于创建对象的函数。对于前面的例子而言，构造函数就是Object().
  * hasOwnProperty(propertyName):用于检查给定的属性在当前对象实例中（而不是在实例的原型中）是否存在。其中，作为参数的属性名（propertyname）必须以字符串形式指定
  * isPrototypeOf(object):用于检查传入的对象是否是传入对象的原型
  * propertyIsEnumerable(propertyName):用于检查给定的属性是否能够使用for-in语句来枚举
  * toLocaleString():返回对象的字符串表示，该字符串与执行环境的地区对应
  * toString():返回对象的字符串表示
  * valueOf():返回对象的字符串，数值，或布尔值表示

  *由于在ECMAScript中Object是所有对象的基础，因此所有对象都具有这些基本的属性和方法*

  **with语句**

  with语句的作用是将代码的作用域设置到一个特定的对象中。with语句的语法如下：

  ```
  with(expression) statement;
  ```
  定义with语句的目的主要是为了简化多次编写同一个对象的工作，如下面的例子：
  ```
  var qs = location.search.substring(1);
  var hostName = location.hostname;
  var url = location.href;
  ```

  上面几行代码都包含location对象。如果使用with语句，可以把上面的代码改写成如下所示：

  ```
  with(loacation){
      var qs = search.substring(1);
      var hostName = hostname;
      var usr = href;
  }
  ```

  *严格模式下不允许使用with语句，否则将视为语法错误*

  *由于大量使用with语句会导致性能下降，同时也会给调试代码造成困难，因此在开发大型应用程序时，不建议使用with语句*
