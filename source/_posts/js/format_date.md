---
title: 格式化日期对象
date: 2017/1/20 22:21:13
tags: Date
categories: JavaScript
---

#### 代码

<!-- more -->
 ```js
    /**
     * 把日期对象转化为指定格式
     * @param  {[Object]} date [日期对象]
     * @param  {[String]} fmt  [例如 'yyyy-MM-dd hh:mm']
     * @return {[String]}      [2017-01-01 01:01]
     */
    
    function formatDate(date, fmt) {
        if (/(y+)/.test(fmt)) {
            fmt = fmt.replace(RegExp.$1, (date.getFullYear() + '').substr(4 - RegExp.$1.length))
        }
        let o = {
            'M+': date.getMonth() + 1,
            'd+': date.getDate(),
            'h+': date.getHours(),
            'm+': date.getMinutes(),
            's+': date.getSeconds()
        }
        for (let k in o) {
            if (new RegExp(`(${k})`).test(fmt)) {
                let str = o[k] + ''
                fmt = fmt.replace(RegExp.$1, (RegExp.$1.length === 1) ? str : padLeftZero(str))
            }
        }
        return fmt
    }

    function padLeftZero(str) {
        return ('00' + str).substr(str.length)
    }

```  

#### 如何使用

```js
    formatDate(new Date(),'yyyy-MM-dd hh:mm')
    //"2017-01-20 21:45"

    formatDate(new Date(),'yy-MM-dd hh:mm')
    //"17-01-20 21:45"

    formatDate(new Date(),'yy年MM月dd日 hh分mm秒')
    //"17年01月20日 45分47秒"
 ```
