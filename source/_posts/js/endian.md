---
title: JS字节序相关
date: 2020/7/30 22:22:10
tags: [JavaScript]
categories: JavaScript
---

### 字节序分2种
1. Little endian：小端字节序, 将低序字节存储在起始地址
2. Big endian：大端字节序, 将高序字节存储在起始地址

### JS里面的体现: 同一段数据用不同视图读取
```
const uint8 = new Uint8Array([1, 2]);
// Uint8Array(2) [1, 2]

const uint16 = new Uint16Array(Uint8.buffer);
// Uint16Array [513]
```
上面代码生成一个 2 个长度的Uint8 TypedArray，然后在它的buffer基础上，建立了一个 16 位整数的视图。
那么这段数据对应的二进制应该是  `00000001 00000010`
```js
0b0000000100000010
// 258
```
用16位无符号整数读出来应该是 `0b0000000100000010`, 应该是258， 为什么是 513呢 ？ 

### 解释： 
这说明本电脑采用的小端字节序（little endian），相对重要的字节排在后面的内存地址，相对不重要字节排在前面的内存地址， 即` 00000010 00000001` 
```js
0b0000001000000001
// 513
```
那么如果想手动指定字节序呢 ?

### DataView 视图: 
1. 支持多种类型读写
2. 支持设置字节序

DataView视图提供更多操作选项，而且支持设定字节序。
默认情况下，DataView的get方法使用大端字节序解读数据，如果需要使用小端字节序解读，必须在get方法的第二个参数指定true。

```
const dv = new DataView(uint8.buffer);
dv.getUint16(0)
// 258 大端字节序

dv.getUint16(0, true)
// 513 小端字节序
```
写入数据同理。