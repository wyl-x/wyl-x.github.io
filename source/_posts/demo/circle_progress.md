---
title: 如何实现环形进度条
date: 2017/4/26 22:29:26
tags: [canvas,JavaScript]
categories: JavaScript
---

业务中经常会遇到做进度条的需求，怎么做一个环形进度条呢，下面是一种 canvas 实现方法。

<!-- more -->
### 代码
```js
    /**
     * 环形进度条组件
     * @param  {Object} options 配置项
     */
    function circleProgress(options) {
        var progress = options.progress;
        var speed = options.speed || 30;
        var width = options.width || 200;
        var height = options.height || 200;
        var lineWidth = options.lineWidth || 10;
        var color = options.color || '#5a6'

        if (speed < 1) {
            speed = 1;
        }
        if (speed > 100) {
            speed = 100;
        }

        var percent = 0;
        function draw() {
            percent += speed / 10;
            if (percent > progress) {
                percent = progress;
                cancelAnimationFrame(timer);
            }
            var PI = Math.PI;
            var angle = percent / 100 * 2 * PI - PI / 2;
            var cvs = document.querySelector('.progress');
            cvs.width = width;
            cvs.height = height;
            var ctx = cvs.getContext('2d');
            ctx.lineWidth = lineWidth;
            ctx.strokeStyle = color;
            ctx.clearRect(0, 0, width, height)
            ctx.arc(width / 2, height / 2, width / 2 - lineWidth, -PI / 2, angle);
            ctx.stroke();
            var timer = requestAnimationFrame(draw);
        }

        draw();
    }
```
options分别为：
* progress 进度（必填），如 45表示 45 %
* speed 动画速度
* width 画布宽度
* height 画布高度
* lineWidth 进度条宽度
* color 颜色

### 调用  

#### html
```html
    <canvas class="progress"></canvas>
```
#### js
```js
    circleProgress({
        progress: 75,
        speed: 10,
        width: 300,
        height: 300,
        lineWidth: 10,
        color: 'blue',
    });
```
### DEMO
猛戳地址: [https://wyl-x.github.io/demos/circle_progress.html](https://wyl-x.github.io/demos/circle_progress.html)