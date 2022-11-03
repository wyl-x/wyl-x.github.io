---
title: JS画函数图象
date: 2016/11/20 19:21:23
tags: DEMO
categories: DEMO
---
#### DEMO地址 [http://wylong.site/draw_function.html](http://wylong.site/draw_function.html)
#### JS代码

<!-- more -->
 ```js
    var sin = Math.sin
    var cos = Math.cos

    //生成点
    function drawPoint(x, y) {
        var xx = x + 50
        var yy = -y + 50
        document.write('<span style="background-color:' + color(xx, yy) + ';top:' + yy / 2 + 'vh;left:' + xx / 2 + 'vw;"></span>')
    }

    //颜色
    function color(x, y) {
        var r = parseInt((x + 100) % 256)
        var g = parseInt((y + 80) % 256)
        var b = parseInt((y + 150) % 256)
        return 'rgb(' + r + ',' + g + ',' + b + ')'
    }

    // 画出函数f的极坐标图像
    function draw(f) {
        var r, x, y
        for (var t = 0; t < 100; t += 0.1) { //角度
            r = f(t)
            x = r * cos(t)
            y = r * sin(t)
            drawPoint(x, y)
        }
    }


    var f = function(t) {
        return (Math.sin(5 * t) + 4) * 10

    }

    draw(f)

```  

#### CSS 代码

```css
    span {
        position: fixed;
        width: 10px;
        height: 10px;
        border-radius: 50%;
    }

 ```
