---
title: 怎么理解 JS “一切皆对象”
date: 2017/4/20 23:14:35
tags: JavaScript
categories: JavaScript
---

网上非常多都在说“JavaScript 一切皆对象”，那么怎么理解这句话呢。  
最新的 ECMAScript 标准定义： 
* JS 基本数据类型:  boolean、undefined、number、string、symbol (ECMAScript 6 定义)，按值比较，按值传递；
* 引用数据类型：object ，任何非基本类型的都是对象类型。如 function，array 等，按引用比较，按引用传递。  
<!-- more -->

基本数据类型没有方法和属性，但有时候我们看见可以直接调用string的长度，如
```js
    var str = 'abc';
    console.log(str.length); // 3
    console.log(typeof str); // 'string'
```
基本数据类型不是对象，但是使用基本类型变量可以调用方法是因为产生了包装对象（临时的），我们在读取它的属性的时候，js会把这个string字符串通过new String()方式创建一个字符串对象，有了对象自然就有了属性，但是这个对象只是临时的，一旦引用结束，这个对象就被销毁了。同理，数字、布尔值在读取属性的时候也可以通过自己的构造函数来创建自己的一个临时对象。  
null 是一个关键字，表示“空值”，我们对null执行typeof操作，输出结果是'object'，所以我们可以把null看成一个特殊的对象。  
undefined是另一个表示“空值”特殊值，它表示未定义，当我们对变量只声明没有初始化时，输出为 undefined，当我们引用一个不存在的属性时，输出也为 undefined，但是undefined没有包装对象，应该不能称之为对象。