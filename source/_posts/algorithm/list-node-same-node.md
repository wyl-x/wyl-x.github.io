---
title: 找到两个单向链表相交的第一个公共节点
date: 2021/8/5 23:20:13
tags: [JavaScript]
categories: algorithm
---

## 方法1
两层for循环，遍历两个链表，判断第一个链表里面的节点是否在第二个链表里面，时间复杂度O(m*n)

## 方法二
分别把两个链表的节点放入两个栈中，从两个栈的栈顶开始比较，直到找到最后一个相同的节点，就是他们的公共点。
```js
function findSameNode(node1, node2) {
  let result = null;

  const stack1 = [];
  const stack2 = [];

  let head1 = node1;
  let head2 = node2;
  while (head1) {
    stack1.unshift(head1);
    head1 = head1.next;
  }
  while (head2) {
    stack2.unshift(head2);
    head2 = head2.next;
  }

  for (let i = 0; i < stack1.length; i++) {
    const n1 = stack1[i];
    const n2 = stack2[i];
    if (n1 !== n2) return result;
    else result = n1;
  }
  return result;
}
```

## 方法三
计算两个链表的长度`len1`, `len2`，长的链表指针走 `Math.abs(len1 - len2)` 步，然后两个链表同时遍历，找到第一个相同的节点
```js
function findSameNode2(node1, node2) {
  let len1 = 0;
  let len2 = 0;
  let head1 = node1;
  let head2 = node2;
  while (head1) {
    len1++;
    head1 = head1.next;
  }

  while (head2) {
    len2++;
    head2 = head2.next;
  }

  let long = len1 > len2 ? node1 : node2;
  let short = len1 > len2 ? node2 : node1;
  let delta = Math.abs(len1 - len2);
  while (delta--) {
    long = long.next;
  }

  let shortLength = Math.min(len1, len2);
  while (shortLength--) {
    if (long === short) return long;
    long = long.next;
    short = short.next;
  }

  return null;

}
```