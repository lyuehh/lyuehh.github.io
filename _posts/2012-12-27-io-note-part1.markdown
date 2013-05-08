---
layout: post
title: Io学习笔记一
date: 2012-12-27 23:42
comments: true
categories: io
---


## 创建1个对象
```
Io> A := Object clone
```
:= 表示不存在则创建，存在则复制  
= 不存在时赋值会报错  
对象在前，空格，发送的消息，空格相当于是'.'  
`Object clone` 在js里相当于 `Object.clone()`
## 给对象槽赋值
```
Io> A say := "I'm saying, haha"
```
相当于js里的
```
A = {
  say: "I'm saying, haha"
};
```
获取槽里的值
```
Io> A say
```
相当于js里的`A.say`
## 查看所有槽
```
Io> A slotNames
==> list(type, say)
```
相当于js的里的`Object.values(A)`
## 继承
```
Io> A := Object clone
Io> A say:= "say, haha"
Io> Car := A clone
Io> Car say
==> say haha
```
car里没有say，它就直接把say消息直接转发给A
```
Io> fa := Car clone
Io> fa slotNames
==> list()
Io> fa type
==> Car
```
io里约定大写字母开头的是类型，小写字母开头的也是对象，但不是类型  
在io里，对象是槽的容器，发送槽名给槽可以获得该槽，如果该槽不存在，则调用父对象的槽。  
## 方法
```
method("a, haha" println)
```
创建一个方法，类似js里的
```
function() {
  console.log('a, haha');
}
```
```
Io> method() type
==> Block
```
方法的类型是Block
```
Io> Car drive := method("Drive" println)
==> method(
    "Drive" println
)
```
给Car添加一个方法 drive，相当于js里的
```
Car.drive = function() {
  console.log('Drive');
};
```
因为fa继承Car，所以fa可以直接调用drive
```
Io> fa drive
Drive
==> Drive
```
## 获取槽中的内容
可以给对象发送getSlot来获取槽中的内容，无论是变量还是方法  
如果该槽不存在，getSlot会提供父对象的槽
```
Io> fa getSlot("drive")
==> method(
    "Drive" println
)
IO> fa getSlot("type")
==> Car
```
## 获取对象的原型
可以给对象发送proto获取对象的原型
```
Io> fa proto
==> Car_0x7f81f8caa5a0:
  drive = method(…)
  type = "Car"
Io> Car proto
==> A_0x7f81f8e70230:
  say = "say haha"
  type = "A"
```
## 主命名空间
Lobby是主命名空间，包含了所有的已命名对象
```
Io> Lobby
==> Object_0x7f81f8c1ba20:
  A = A_0x7f81f8e70230
  Car = Car_0x7f81f8caa5a0
  Lobby = Object_0x7f81f8c1ba20
  Protos = Object_0x7f81f8c1ad00
  _ = Object_0x7f81f8c1ba20
  exit = method(…)
  fa = Car_0x7f81f8e83840
  forward = method(…)
  set_ = method(…)
```
你可以看到exit的实现，forward，Protos和我们自定义的东西
查看exit的实现
```
Io> Lobby getSlot("exit")
==> # [unlabeled]:0
method(
    CLI stop
)
```
Protos的实现
```
Io> Lobby getSlot("Protos")
==> Object_0x7f81f8c1ad00:
  Addons = Object_0x7f81f8c1be30
  Core = Object_0x7f81f8c1b9b0
```
## 基本准则
* 所有事物都是对象
* 所有与对象的交互都是消息
* 不需要实例化类，而是复制那些叫做原型的对象
* 对象会记住它的类型
* 对象有槽
* 槽包含对象(包括方法对象)
* 消息返回槽中的值，或调用槽中的方法
* 如果对象无法响应某消息，它会把该消息发送给自己的原型

# 列表和映射
Io包含了几种类型的集合。列表(list) 是任意类型对象的有序集合，所有列表的原型都是List对象。
而Map对象是键值对的原型，成为映射，和ruby的散列表一样。
## 创建列表
```
Io> todos := list("eat", "sleep")
==> list(eat, sleep)
Io> todos size
==> 2
Io> todos append("talk")
==> list(eat, sleep, talk)
```
Io在表示列表时有一种快捷方式，由Object对象提供的list方法。它能把传入方法的参数包装起来形成列表，使用list方法，我们可以这样创建列表:
```
Io> Io> list(1, 2, 3, 4)
==> list(1, 2, 3, 3, 4)
```
对列表进行数学运算，或是当做其他数据类型(比如栈)，List对象也提供了各种简便方法:
```
Io> list(1, 2, 3, 4) average
==> 2.5
Io> list(1, 2, 3, 4) sum
==> 10
Io> list(1, 2, 3, 4) at(1)
==> 2
Io> list(1, 2, 3, 4) append(4)
==> list(1, 2, 3, 4, 4)
Io> list(1, 2, 3, 4) pop
==> 4
Io> list(1, 2, 3, 4) prepend(0)
==> list(0, 1, 2, 3, 4)
Io> list() isEmpty
==> true
```
另一种主要集合是Map对象，像是ruby的散列表，这个没有语法糖，必须用API操作:
```
Io> p := Map clone
==> Map_0x7f81f8e4d8d0:
Io> p atPut("name", "zhangsan")
==> Map_0x7f81f8e4d8d0:
Io> p at("name")
==> zhangsan
Io> p atPut("style", "rock")
==> Map_0x7f81f8e4d8d0:
Io> p asObject
==> Object_0x7f81f983e170:
  name = "zhangsan"
  style = "rock"
Io> p asList
==> list(list(name, zhangsan), list(style, rock))
Io> p keys
==> list(name, style)
Io> p size
==> 2
```
散列表和Io对象很像，散列表的键就是一个个绑定了值的槽。
## 布尔值 true false nil 和单例
```
Io> 4 < 5
==> true
Io> 4 <= 3
==> false
Io> true and false
==> false
Io> true and true
==> true
Io> true or true
==> true
Io> 4 < 5 and 6 < 7
==> true
Io> true and 6
==> true
Io> true and 0
==> true
```
和ruby一样，0是true，而true又是什么呢
```
Io> true pro to
==> Object_0x7f81f8c04010:
                   = Object_()
  != = Object_!=()
  - = Object_-()
… 省略一堆
```
```
Io> true clone
==> true
Io> false clone
==> false
Io> nil clone
==> nil
```
true, false, nil都是单例，复制它们，返回的只是单例对象的值
## 创建自己的单例对象
```
Io> S := Object clone
==> S_0x7f81f8ef0f40:
  type = "S"
Io> S clone := S
==> S_0x7f81f8ef0f40:
  clone = S_0x7f81f8ef0f40
  type = "S"
Io> S clone
==> S_0x7f81f8ef0f40:
  clone = S_0x7f81f8ef0f40
  type = "S"
Io> s1 := S clone
==> S_0x7f81f8ef0f40:
  clone = S_0x7f81f8ef0f40
  type = "S"
Io> s2 := S clone
==> S_0x7f81f8ef0f40:
  clone = S_0x7f81f8ef0f40
  type = "S"
Io> s1 == s2
==> true
```
我们重新定义了S 的clone方法，让它返回本身，这样就形成了一个单例
## 小心
Io里你几乎可以改变任何对象上的任何一个槽，比如这样
```
Io> Object clone := "haha"
```
因为你覆盖了Object上的clone方法，从此你无法再创建对象了，只能终止进程重新开始。
当然这些自由在实现特定领域语言(DSL: domian-specific language)时非常方便。
## 基础类型的方法
```
Io> true slotNames
==> list(asSimpleString, asString, not, ifFalse, else, ifTrue, or, type, justSerialized, clone, elseif, then)
Io> Object slotNames
==> list(slotSummary, ownsSlots, and, apropos, foreachSlot, performWithArgList, coroWith, <, actorRun, removeAllSlots, for, isTrue, clone, become, !=, write, switch, setSlotWithType, method, ancestors, futureSend, resend, isActivatable, lazySlot, list, justSerialized, evalArg, uniqueId, @@, do, thisContext, deprecatedWarning, setProto, println, hasProto, writeln, setSlot, handleActorException, inlineMethod, ifNonNil, isKindOf, setIsActivatable, removeAllProtos, coroFor, pause, continue, ifNil, stopStatus, prependProto, ancestorWithSlot, print, protos, evalArgAndReturnSelf, doString, type, ?, return, break, >, message, ==, currentCoro, slotNames, hasLocalSlot, while, perform, serialized, ifNonNilEval, wait, asString, returnIfNonNil, getLocalSlot, or, getSlot, asSimpleString, compare, coroDoLater, hasDirtySlot, slotDescriptionMap, removeProto, appendProto, in, isNil, uniqueHexId, loop, lexicalDo, not, .., doRelativeFile, try, launchFile, , yield, isError, ifNilEval, init, evalArgAndReturnNil, doFile, serializedSlotsWithNames, argIsActivationRecord, returnIfError, isIdenticalTo, super, isLaunchScript, serializedSlots, cloneWithoutInit, hasSlot, contextWithSlot, thisLocalContext, >=, if, relativeDoFile, memorySize, <=, asyncSend, thisMessage, @, markClean, coroDo, slotValues, -, doMessage, proto, ifError, newSlot, updateSlot, removeSlot, shallowCopy, block, actorProcessQueue, raiseIfError, setProtos, argIsCall)
Io> List slotNames
==> list(isEmpty, remove, exSlice, sortByKey, mapFromKey, ListCursor, map, atPut, uniqueCount, contains, itemCopy, copy, sortInPlace, removeAll, asMap, sort, sliceInPlace, insertBefore, rest, containsAny, asString, min, removeSeq, cursor, intersect, reverseForeach, foreach, empty, sortKey, fromEncodedList, with, removeAt, justSerialized, max, asJson, pop, size, selectInPlace, average, third, push, reduce, detect, insertAfter, at, appendIfAbsent, last, sum, select, difference, removeFirst, indexOf, groupBy, asMessage, reverse, union, slice, isNotEmpty, mapInPlace, append, preallocateToSize, reverseInPlace, asSimpleString, removeLast, flatten, sortInPlaceBy, prepend, asEncodedList, atInsert, appendSeq, insertAt, unique, reverseReduce, join, second, swapIndices, containsAll, first, sortBy, containsIdenticalTo, setSize, capacity)
Io> Map slotNames
==> list(map, at, atPut, asObject, reverseMap, merge, asList, detect, isNotEmpty, keys, removeAt, hasValue, isEmpty, mergeInPlace, select, hasKey, empty, foreach, with, justSerialized, asJson, atIfAbsentPut, addKeysAndValues, size, values)
```
