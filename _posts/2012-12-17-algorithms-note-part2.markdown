---
layout: post
title: 算法学习笔记之二 - 线性表
date: 2012-12-17 22:39
comments: true
categories: algorithms
---

线性表是由有限个元素组成的有序队列，有序是指线性表中存在唯一的第一个和最后一个元素。  
线性表可以用数组来描述，也可以用链表来描述，前者为顺序存储，而后者为链式存储。  
线性表的常见操作为添加，删除，插入，查找，遍历，统计。  
下面就用javascript分别实现。  

## 线性表的数组实现
数组实现的复杂度为:

* 添加: 添加到数组末尾,复杂度为O(1)
* 插入: 如果插入到最后，则相当于是添加，复杂度是O(1)；如果是插入到数组的开头，
那么后面的节点都要往后移动一位，所以复杂度是O(N)
* 删除: 和插入类似，删除最后一个节点，为O(1);删除其他，为O(N)
* 按照序号查找: 因为按顺序存储，所以复杂度为O(1)
* 按元素内容查找: 需要遍历，复杂度为O(N)

### 插入的实现
从插入的index开始，将后面代码的每个元素向右移动一位，将index那个位置空出来，
放置item即可。

### 删除的实现
从index开始，将后面的元素向左移动一位。

```javascript part2: array_list.js
/*
 * array_list
 */

'use strict';

function ArrayList() {
  this.data = [];
  this.length = 0;
}

ArrayList.prototype = {
  constructor: ArrayList,
  append: function (item) {
    this.data[this.length] = item;
    this.length ++;
  },
  remove2: function (index) {
    this.check(index);
    var item = this.data[index];
    this.data.splice(index,1);
    this.length --;
    return item;
  },
  remove: function (index) {
    this.check(index);
    var item = this.data[index];
    for (var i = index; i < this.data.length; i += 1) {
      this.data[i] = this.data[i+1];
    }
    // TODO js删除数组元素只能用splice方法，不存在的元素是undefined
    // this.data.splice(this.length,1); // 这一句话没作用？？
    this.length --;
    return item;
  },
  size: function () {
    return this.length;
  },
  insert2: function (index, item) {
    this.check(index);
    this.data.splice(index, 0, item);
    this.length ++;
  },
  insert: function (index, item) {
    this.check(item);
    for (var i = this.length; i >= index; i -= 1) {
      this.data[i] = this.data[i-1];
    }
    this.data[index] = item;
    this.length ++;
  },
  check: function (index) {
    if(typeof index !== 'number') {
      throw 'index should be number';
    }
    if(index < 0 || index > this.length) {
      throw 'index should large than 0 and less than this.size()';
    }
  }
};

module.exports = ArrayList;
```

## 线性表的链表实现

链表是一种递归的数据结构，它或者为空(null)，或者是指向一个节点(node)的引用，该节点含有一个元素
和一个指向另一条链表的调用。  
链表包含许多变种，也有很多操作，这里先实现单链表，并且只实现和上面同样的操作。  


## append
创建node，设置node的item为item，判断head是否为null，若为null，则链表为空，设置head为node；
否则，设置current为head，循环current的next直到current的next为null，这是current就是最后一个节点，
设置current的next为node，然后让N加1即可。  

## get
首先检查index参数，设置current为head，设置i为0；循环i++，设置current为current的next，当i等于index时，
表示current就是索引为index的节点，返回current.item即可。  

## remove
保存current为head，如果index为0，设置head为current的next即可，否则，循环i++，设置previous为current，
current为current的next，当i等于index时，previous为所查找节点的上个节点，设置previous的next为current的next，
就表示删除了current节点。  

## size
设置current为head，循环current，将count加1，设置current为current的next，当current为null时，
表示循环到了尽头，返回count即可。  


### 代码

```javascript
/*
 * linkedlist
 */

'use strict';

function Node(item) {
  this.item = item;
  this.next = null;
}

function LinkedList() {
  this.head = null;
}

LinkedList.prototype = {

  constructor: LinkedList,
  append: function (item) {
    var node = new Node(item);

    if(this.head === null) {
      this.head = node;
    } else {
      var current = this.head;
      while(current.next) {
        current = current.next;
      }
      current.next = node;
    }
  },
  remove: function (index) {
    this.check(index);
    var current = this.head,
      previous,
      i = 0;
    if(index === 0) {
      this.head = current.next;
    } else {
      while(i++ < index) {
        previous = current;
        current = current.next;
      }
      previous.next = current.next;
    }
    return current.item;
  },
  size: function () {
    var current = this.head,
      i = 0;
    while(current) {
      i++;
      current = current.next;
    }
    return i;
  },
  get: function (index) {
    this.check(index);
    var current = this.head,
      i = 0;
    while(i++ < index) {
      current = current.next;
    }
    return current.item;
  },
  check: function (index) {
    if(typeof index !== 'number') {
      throw 'index should be number';
    }
    if(index < 0 || index > this.length) {
      throw 'index should large than 0 and less than this.size()';
    }
  }
};

module.exports = LinkedList;

```

## 双链表
双向链表的每个节点有2个指针，一个指向后继结点，一个指向前驱节点，使用双向链表，可以从
链表任一节点出发，向前或者向后访问节点。  

### add操作
根据item创建node，如果当前链表为空，则将head和tail指向node；否则，将tail的next指向node，
将node的prev指向tail，将tail指向node。然后将length加1。

### get操作
将current指向head，设置i为0；循环i<index，将current指向current的next，然后将i加1，
当i等于index时，表明当前的current即为查找的节点，返回current.item。

### remove操作
将current指向head，设置i为0；当index为0时，表明将移除head所指向的节点，将head指向current的next，
这时需要判断head是否为空，如果为空，则表明链表只有1个元素，这时需要将tail也设置为null，
否则将head的prev指向null；当index和lengt-1相等，表明将移除tail所指向的节点，将current指向tail，
将tail指向current的prev,将tail的next指向null，(这里current的用途是保存旧的尾节点);
如果不属于以上两种情况，循环i<index,将current指向current的next，然后将i加1，当i等于
index时，将current的prev的next指向current的next即可。

### 代码
```javascript
function Node(item) {
  this.item = null;
  this.prev = null;
  this.next = null;
}

function DoubleLinkedList() {
  this.head = null;
  this.tail = null;
  this.length = 0;
}

DoubleLinkedList.prototype = {

  constructor: DoubleLinkedList,
  add: function(item) {
    var node = new Node(item);

    if(this.length === 0) {
      this.head = node;
      this.tail = node;
    } else {
      this.tail.next = node;
      node.prev = this.tail;
      this.tail = node;
    }
    this.length++;
  },
  get: function (index) {
    this.check(index);
    var current = this.head,
      i = 0;

      while(i < index) {
        current = current.next;
        i++;
      }
      return current.item;
  },
  remove: function (index) {
    var current = this.head,
      i = 0;

    if(index === 0) {
      this.head = current.next;

      if(!this.head) {
        this.tail = null;
      } else {
        this.head.prev = null;
      }
    } else if(index === this.length - 1){
      current = this.tail;
      this.tail = current.prev;
      this.tail.next = null;
    } else {
      while(i < index) {
        current = current.next;
        i++;
      }
      current.prev.next = current.next;
    }
    this.length--;
  },
  size: function () {
    return this.length;
  },
  toArray: function () {
    var ret = [],
      current = this.head;

    while(current) {
      ret.push(current.item);
      current = current.next;
    }
    return ret;
  },
  toString: function () {
    return this.toArray().toString();
  },
  check: function (index) {
    if(typeof index !== 'number') {
      throw 'index should be number';
    }
    if(index < 0 || index > this.length) {
      throw 'index should large than 0 and less than this.size()';
    }
  }

};

module.exports = DoubleLinkedList;
```

## Gitbub
测试代码位于Github, <https://github.com/lyuehh/algorithms-note-js>,安装mocha，然后在目录执行mocha即可。

