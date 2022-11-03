---
title: JS常见排序算法
date: 2016/12/29 18:34:16
tags: [JavaScript,排序]
categories: algorithm
---

学习写一下排序算法。  
<!-- more -->
### 冒泡排序
 ```js
    function bubbleSort(arr) {
        for (let i = 0; i < arr.length; i++) {
            let swapped // 检测是否发生交换
            for (let j = 0; j < arr.length - i - 1; j++) {
                // 如果相邻两项左边>右边，则交换
                if (arr[j] > arr[j + 1]) {
                    // ES6 交换变量：[a, b]=[b, a]
                    [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]]
                    swapped = true
                }
            }
            if (!swapped) {
                // 若某一次未交换，返回数组
                return arr
            }
        }
    }

```
### 选择排序
```js
    function selectSort(arr) {
        for (let i = 0; i < arr.length - 1; i++) {
            let minIndex = i // 最小值的 Index
            for (let j = i + 1; j < arr.length; j++) {
                if (arr[j] < arr[minIndex]) {
                    minIndex = j
                }
            }
            if (i !== minIndex) {
                // 交换
                [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]]
            }
        }
        return arr
    }
    
```
### 快排
```js
    function quickSort(arr) {
        let choosed = arr[0]
        let left = [] // 存储比 choosed 小的值
        let right = [] // 存储比 choosed 大的值
        if (arr.length < 2) {
            return arr
        }
        for (let i = 1; i < arr.length; i++) {
            if (arr[i] <= choosed) {
                left.push(arr[i])
            } else {
                right.push(arr[i])
            }
        }
        // 递归，拼接
        return quickSort(left).concat(choosed).concat(quickSort(right))
    }
```
这种方法很容易理解，但每次生成两个数组，再加上递归，空间复杂度太高
### 快排优化版
```js
    function quickSort(arr, start, end) {
        if (start == undefined) {
            start = 0
        }
        if (end == undefined) {
            end = arr.length - 1
        }
        if (end - start < 1) {
            return arr
        }
        var left = start
        var right = end
        var choose = arr[start]
        
        while (left < right) {
            while (arr[right] >= choose && left < right) {
                right--
            }
            while (arr[left] <= choose && left < right) {
                left++
            }
            [arr[left], arr[right]] = [arr[right], arr[left]]
        }
        
        [arr[left], arr[start]] = [arr[start], arr[left]]
        quickSort(arr, start, left - 1)
        quickSort(arr, left + 1, end)
        return arr
    }
```

