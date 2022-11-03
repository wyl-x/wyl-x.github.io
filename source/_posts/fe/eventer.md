---
title: JS模拟自定义事件
date: 2016/12/23 23:31:16
categories: JavaScript
---

通过JS模拟事件的绑定、触发和取消绑定。  
<!-- more -->
代码
 ```js
    //模拟事件绑定 
    class Eventer {
        constructor() {
            this.methods = {}
        }

        on(type, handler) {
            this.methods[type] = this.methods[type] || []
            this.methods[type].push(handler)
            return this
        }

        trigger(type, data) {
            this.methods[type] && this.methods[type].forEach(fn => {
                fn.call(this, data)
            })
            return this
        }

        remove(type) {
            delete this.methods[type]
            return this
        }
    }

```
函数内部返回 this 对象可实现链式调用。  

如何使用

```js
    let e=new Eventer()

    //绑定click事件
    e.on('click',function(){
        console.log('CLICKED')
    })

    //触发click事件
    e.trigger('click')

    //移除事件
    e.remove('click')
    
 ```
