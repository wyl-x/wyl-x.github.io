---
title: getter和setter
date: 2017/1/13 19:22:56
tags: JavaScript
categories: JavaScript
---

目前流行的 “双向绑定”，MVVM之类的库有很多，其中Vue.js 是采用 Object.defineProperty 的 getter 和 setter，并结合观察者模式来实现数据绑定的。那么getter和setter怎么用呢。

<!-- more -->
```js
    var obj = {
        log: ['test'],
        get latest() {
            if (this.log.length == 0) {
                return undefined
            }
            return this.log[this.log.length - 1]
        },
        set latest(value) {
            this.log.push(value)
        }
    }
    console.log(obj.latest) // "test"
    obj.latest = 'latest'
    console.log(obj.log) // ['test', 'latest']
```
对于已存在的对象,使用 `Object.defineProperty`
```js
    var o = {
        log: ['test']
    }

    Object.defineProperty(o, 'latest', {
        enumerable: false,
        configurable: false,
        get: function() {
            if (this.log.length == 0) {
                return undefined
            }
            return this.log[this.log.length - 1]
        },
        set: function(value) {
            this.log.push(value)
        }
    })
```
用来实现私有变量
```js
    var person = function() {
        var _name = ''
        var _age = 0
        var obj = {}
        Object.defineProperty(obj, 'name', {
            configurable: true,
            enumerable: true,
            get: function() {
                return _name
            },
            set: function(n) {
                _name = n
            }
        })
        Object.defineProperty(obj, 'age', {
            configurable: true,
            enumerable: true,
            get: function() {
                return _age
            },
            set: function(a) {
                _age = a
            }
        })
        return obj
    }()
```

