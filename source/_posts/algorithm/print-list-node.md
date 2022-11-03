---
title: 链表打印
date: 2021/7/29 19:22:13
tags: [JavaScript]
categories: algorithm
---

```js
// 递归
function printListNodeFromTail(head) {
  if (!head) return;
  printListNodeFromTail(head.next);
  console.log(head.value);
  return head;
}

// 非递归
function printListNodeFromTail2(head) {
  const listNodeArray = [];
  while (head) {
    listNodeArray.unshift(head);
    head = head.next;
  }

  listNodeArray.forEach(item => console.log(item.value));
}
```