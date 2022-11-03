---
title: JS实现简易JSON Parser
date: 2016/11/29 20:01:14
tags: [JSON,JavaScript]
categories: JavaScript
---

ES5提供一个内置的（全局）JSON对象，可用来序列化（JSON.stringfy）和反序列化（parse）对象为JSON格式绑定，下面是自己尝试实现的一个JSON parser函数。

<!-- more -->
### 代码
    ```js
        /**
         * [解析JSON数据为JS对象]
         * @param  {String} str JSON数据
         * @return {Object} 返回JS对象
         */
        function parseJson(str) {
            var json = str
            var i = 0
            return parse()

            function parse() {
                if (!isNaN(json[i])) {
                    return parseNumber()
                }
                if (json[i] === '"') {
                    return parseString()
                }
                if (json[i] === 't') {
                    return parseTrue()
                }
                if (json[i] === 'f') {
                    return parseFalse()
                }
                if (json[i] === 'n') {
                    return parseNull()
                }
                if (json[i] === '[') {
                    return parseArray()
                }
                if (json[i] === '{') {
                    return parseObject()
                }
            }
            // 解析 number
            function parseNumber() {
                var start = i
                while (true) {
                    i++
                    if (isNaN(json[i])) {
                        return Number(json.slice(start, i))
                    }
                }
            }
            // 解析 string
            function parseString() {
                var start = i + 1
                var index = json.indexOf('"', start)
                var string = json.slice(start, index)
                i = index + 1
                return string
            }
            // 解析 true
            function parseTrue() {
                i = i + 4
                return true
            }
            // 解析 false
            function parseFalse() {
                i = i + 5
                return false
            }
            // 解析 null
            function parseNull() {
                i = i + 4
                return null
            }
            // 解析 array
            function parseArray() {
                var result = []
                i++
                while (true) {
                    if (json[i] === ']') {
                        i++
                        break
                    }
                    result.push(parse())
                    if (json[i] == ',') {
                        i++
                    }
                }
                return result
            }
            // 解析 object
            function parseObject() {
                var result = {}
                i++
                var key
                var value
                while (true) {
                    key = parseString()
                    i++
                    value = parse()
                    result[key] = value
                    if (json[i] == '}') {
                        break
                    } else {
                        i++
                        continue
                    }
                }
                return result
            }
        }
    ```
### 测试
    ```js
        var json = '{"foo":true,"bar":2878,"str":"abcdef","a":null,"arr":[true,1,2],"obj":{"foo":"bar","ffo":"abc"}}'

        parseJson(json)

        //Object {foo: true, bar: 2878, str: "abcdef", a: null, arr: Array(3)…}
        
    ```
