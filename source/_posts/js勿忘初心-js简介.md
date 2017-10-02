---
title: js基础学习
date: 2017-09-30 13:59:25
tags: js-勿忘初心
categories: js之路
---

### 重新出发


大概做了一年的前端吧，一直都是针对问题然后解决问题，从未真正地去学学js基础，是时候好好学学js了



- - -


### javascript简介

**js简史**
js之前创立的目的在于简化浏览器与服务端之间的数据验证

Netscape为了搭上媒体热炒java的顺风车，临时把LiveScript改名为JavaScript

当时存在两个版本：
1. Netscape Navigator中的Javacript 
2. Internet Explorer中的JScript

而当时还没有规定的js的语法和特性，这就导致了兼容性问题

1998年，浏览器开发商就开始致力于将ECMAScrip作为各自js实现的基础，也在不同程度上取得了成功

**js实现**

一个完整的js实现应该由下列三个不同的部分组成
* 核心（ECMAScript）
* 文档对象模型（DOM）
* 浏览器对象模型（BOM）
由ECMA-262定义的ECMAScript与Web浏览器没有依赖关系，我们常见的web浏览器只是ECMAScript实现可能的宿主环境之一
其他宿主环境包括Node和Adobe Flash
ECMAScript规定了语言的下列组成部分
* 语法
* 类型
* 语句
* 关键字
* 保留字
* 操作符
* 对象

**文档对象模型**

文档对象模型是针对XML但经过扩展勇于html的应用程序编程接口。DMO把真个页面映射为一个多层节点结构

``` 
<html>
       <head>
          <title>Sample Page</title>
       </head>
       <body>
          <p>Hello World</p>
       <body>
</html>
```

借助DOM提供的API，开发人员可以轻松自如地删除，添加，替换或修改任何节点

这个时候人们真正担心的是，如果不对Netscape和微软加以控制，Web领域就会出现技术上的两强割据，浏览器互不兼容的局面，此时，负责制定Web通信标准的W3C开始着手规划DOM

*注意：DOM并不只是针对js的，很多别的语言也都实现了DOM，不过，在web浏览器中，基于ECMAScript实现的DOM的确已经成为JavaScript这门语言的一个重要组成部分*    

DOM级别：
 * 1级：分为DOM核心和DOM HTML:核心规定的是如何映射基于XML的文档结构，DOM HTML则是在DOM核心的基础上加以扩展，添加了针对HTML的对象和方法
 * 2级：在原来DOM的基础上又扩充了布标和用户界面事件，范围，遍历等细分模块
 * 3级：进一步扩展了DOM，引入了以统一方式加载和保存文档的方法，新增了验证文档的方法

 **浏览器对象模型（BOM）**
 
 开发人员可以使用BOM控制浏览器显示的页面意外的部分。而BOM与众不同的地方。还是它作为js实现的一部分但却没有相关的标准。*这个问题在HTML5中得到了解决，HTML5致力于把很多BOM功能写入正式规范。HTML5帆布后。很多关于BOM的困惑烟消云散*

 算作BOM的扩展：
  * 弹出新浏览器窗口的功能
  * 移动，缩放和关闭浏览器窗口的功能
  * 提供浏览器详细信息的navigator对象
  * 提供浏览器岁加载页面的详细信息的location对象
  * 提供用户显示器分辨率详细信息的screen对象
  * 对cookies的支持
  * 像XMLHttpRequest和IE的ActiveXObject这样的自定义对象

  ## 小结

  JavaScript是一种专为与网页交互而设计的脚本语言，由下列三个不同的部分组成

  * ECMAScript，由ECMA-262定义，提供核心语言功能
  * 文档对象模型（DOM），提供访问和操作网页内容的方法和接口
  * 浏览器对象模型（BOM），提供与浏览器交互的方法和接口




