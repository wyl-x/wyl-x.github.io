---
title: 反转链表
date: 2021/7/29 20:34:16
tags: [JavaScript]
categories: algorithm
---

### 反转链表, 大致有递归和非递归方法
```js
// 定义链表结构为
class ListNode {
  constructor(value = null) {
    this.value = value;
    this.next = null;
  }

  /**
   * 为了方便调试，增加一个打印方法
   * 打印出来像这样: 1->2->3
   */
  print() {
    let result = this.value;
    let head = this;
    while (head.next) {
      result += '->' + head.next.value;
      head = head.next;
    }
    console.log(result);
  }
}

/**
 * 创建长度为 length 的链表
 * @param length
 * @returns {ListNode}
 */
function createListNode(length) {
  if (length <= 0) return null;
  const node = new ListNode(length);
  node.next = createListNode(--length);
  return node;
}
// 测试创建链表
const testNone = createListNode(10);
testNone.print();
// 10->9->8->7->6->5->4->3->2->1

// 反转链表递归写法:
/**
 * 反转链表
 * @param node
 * @returns {*}
 */
function reverseNode(node) {
  let result;
  (function reverseNodeAndGetTailNode(node) {
    if (node.next === null) return result = node;
    const next = node.next;
    node.next = null;
    reverseNodeAndGetTailNode(next).next = node;
    return node;
  })(node);

  return result;
}
// 测试反转链表1
const testNoneRevert1 = reverseNode(testNone);
testNoneRevert1.print();
// 1->2->3->4->5->6->7->8->9->10

/**
 * 反转链表，循环迭代写法
 * @param head
 * @returns {*}
 */
function reverseNode2(head) {
  // 记录上一个节点
  let prev = null;

  while (head) {
    const next = head.next;
    head.next = prev;
    prev = head;
    head = next;
  }
  return prev;
}
// 测试反转链表2
const testNoneRevert2 = reverseNode(testNoneRevert1);
testNoneRevert2.print();
// 10->9->8->7->6->5->4->3->2->1
```
--- 
补充
总觉得自己的递归写法有点别扭，每次返回的是尾结点，还得用个变量保存最后的结果，也就是反转后的头结点。
搜了一下其他人的写法，然后自己再写还是差点绕晕了 - - 还是太菜了
```js
function reverseNodeByRecursive(node) {
  if (!node.next) return node;

  const newNode = reverseNodeByRecursive(node.next);
  node.next.next = node;
  node.next = null;

  return newNode;
}

// 测试: 
const testNoneRevert3 = createListNode(10);
testNoneRevert3.print();
// 10->9->8->7->6->5->4->3->2->1

const result = reverseNodeByRecursive(testNoneRevert3)
result.print();
// 1->2->3->4->5->6->7->8->9->10
```