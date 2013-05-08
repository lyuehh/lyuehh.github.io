---
layout: post
title: 算法学习笔记之三 - 栈和队列
date: 2012-12-25 14:41
comments: true
categories: algorithms
---

## 栈
栈是一种基于后进先出(LIFO)策略的集合类型，栈限制了操作只能在一端进行，
但没有限制插入和删除操作进行的时间，只要元素位于栈顶
即可出栈，比如有3个元素a, b, c依次进栈，且元素只允许进一次栈，则可能
的出栈序列有abc, acb, bac, bca, cba 5种。  

栈是一个线性表，所以可以用数组实现，也可以用链表实现。  

下面用链表实现。

```javascript
 /*
 * stack_linkedlist
 */

'use strict';

function Node(item) {
  this.item = item;
  this.next = null;
}

function Stack() {
  this.first = null;
  this.N = 0;
}

/**
 * Stack size
 * @return {Number} size
 */
Stack.prototype.size = function () {
  return this.N;
};

/**
 * Stack is empty or not
 * @return {Boolean} isEmpty
 */
Stack.prototype.isEmpty = function () {
  return this.N === 0;
};

/**
 * Push item into stack
 * @param {Object} item item
 */
Stack.prototype.push = function (item) {
  var oldFirst = this.first;
  this.first = new Node(item);
  this.first.next = oldFirst;
  this.N++;
};

/**
 * Pop item out of stack
 * @return {Object} item
 */
Stack.prototype.pop = function () {
  var item = this.first.item;
  this.first = this.first.next;
  this.N--;
  return item;
};

module.exports = Stack;
```


## 队列

队列是一种基于先进先出(FIFO)策略的集合类型，和栈类似，它可以有数组实现，
也可以由链表实现。  

下面是链表实现。
```javascript
/*
 * queue_linkedlist
 * */

function Node(item) {
  this.item = item;
  this.next = null;
}

function Queue() {
  this.first = null;
  this.last = null;
  this.N = 0;
}

Queue.prototype.size = function () {
  return this.N;
};

Queue.prototype.isEmpty = function () {
  return this.N === 0;
};

Queue.prototype.enqueue = function (item) {
  var oldLast = this.last;
  this.last = new Node(item);
  this.last.next = null;
  if(this.isEmpty()) {
    this.first = this.last;
  } else {
    oldLast.next = this.last;
  }
  this.N++;
};

Queue.prototype.dequeue = function () {
  var item = this.first.item;
  this.first = this.first.next;
  if(this.isEmpty()) {
    this.last = null;
  }
  this.N--;
  return item;
};

module.exports = Queue;
```
