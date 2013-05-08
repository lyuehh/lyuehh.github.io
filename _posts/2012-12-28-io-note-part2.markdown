---
layout: post
title: Io学习笔记之二
date: 2012-12-28 21:15
comments: true
categories: io
---

## 条件和循环

### 无限循环

```
Io> loop("haha..." println)
haha...
haha...
...
```
按Ctrl+C中断

### while循环
```
Io> while(i <= 11, i println; i = i + 1); "The end..." println
1
2
3
4
5
6
7
8
9
10
11
The end...
==> The end...
```

### for循环

```
Io> for(i, 1, 11, i println); "The end..." println
1
2
3
4
5
6
7
8
9
10
11
The end...
==> The end...
```
其中第4个参数为可选的增量，像这样
```
Io> for(i, 1, 11, 2, i println)
1
3
5
7
9
11
==> 11
```
Io允许附加额外参数，所以一定要小心，像这样的代码
```
Io> for(i, 1, 2, i println)
1
2
==> 2
Io> for(i, 1, 2, i println, "extra arg")
2
==> extra arg
```

### if控制结构
```
Io> if(true, "It is true.", "It is false.")
==> It is true.
Io> if(false) then("It is true") else("It is false")
==> nil
Io> if(false) then("It is true." println) else("It is false." println)
It is false.
==> nil
```

### 运算符
Io里你可以直接看到运算符表，像这样
```
Io> OperatorTable
==> OperatorTable_0x7fc123c76200:
Operators
  0   ? @ @@
  1   **
  2   % * /
  3   + -
  4   << >>
  5   < <= > >=
  6   != ==
  7   &
  8   ^
  9   |
  10  && and
  11  or ||
  12  ..
  13  %= &= *= += -= /= <<= >>= ^= |=
  14  return

Assign Operators
  ::= newSlot
  :=  setSlot
  =   updateSlot

To add a new operator: OperatorTable addOperator("+", 4) and implement the + message.
To add a new assign operator: OperatorTable addAssignOperator("=", "updateSlot") and implement the updateSlot message.
```

下面我们自定义一个异或运算符xor，如果只有一个参数为真，
则xor返回true，否则返回false。
```
Io> OperatorTable addOperator("xor", 11)
==> OperatorTable_0x7fc123c76200:
Operators
  0   ? @ @@
  1   **
  2   % * /
  3   + -
  4   << >>
  5   < <= > >=
  6   != ==
  7   &
  8   ^
  9   |
  10  && and
  11  or xor ||
  12  ..
  13  %= &= *= += -= /= <<= >>= ^= |=
  14  return

Assign Operators
  ::= newSlot
  :=  setSlot
  =   updateSlot

To add a new operator: OperatorTable addOperator("+", 4) and implement the + message.
To add a new assign operator: OperatorTable addAssignOperator("=", "updateSlot") and implement the updateSlot message.
```

在11那个位置上可以看到新的运算符，接下来对true和false
两种情况实现xor方法:
```
Io> true xor := method(bool, if(bool, false, true))
==> method(bool, 
    if(bool, false, true)
)
Io> false xor := method(bool, if(bool, true, false))
==> method(bool, 
    if(bool, true, false)
)
```
这就完成了实现
```
Io> true xor true
==> false
Io> true xor false
==> true
Io> false xor true
==> true
Io> false xor false
==> false
```

### 消息
在Io里，几乎一切都是消息，你可以查询任何消息的任何特性，
在对它们执行适当的操作。  

一个消息由三部分组成，发送者(sender)， 目标(target)，
和参数(arguments)。在Io中，消息由发送者发送至目标，
然后由目标执行该消息。  

你可以用call方法访问任何消息的元信息(meta information)。
下面创建2个对象，一个是获得消息的邮局对象postOffice，一个
是发送消息的寄信人mailer。  
```
Io> postOffice := Object clone
==>  Object_0x7fc123eaeeb0:

Io> postOffice packageSender := method(call sender)
==> method(
    call sender
)
```
下面创建发送消息的寄信人
```
Io> mailer := Object clone
==>  Object_0x7fc124876b60:

Io> mailer deliver := method(postOffice packageSender)
==> method(
    postOffice packageSender
)
```
它有一个槽-deliver，该槽发送一个packageSender消息给postOffice。
现在我们有了一个可以发送消息的mailer对象。
```
Io> mailer deliver
==>  Object_0x7fc124876b60:
  deliver          = method(...)
```
deliver方法是发送消息的对象，我们还可以获取目标，像下面这样
```
Io> postOffice messageTarget := method(call target)
==> method(
    call target
)
Io> postOffice messageTarget
==>  Object_0x7fc123eaeeb0:
  messageTarget    = method(...)
  packageSender    = method(...)
```
这里的目标是邮局postOffice，我们还可以获取原消息名和参数。
```
Io> postOffice messageArgs := method(call message arguments)
==> method(
    call message arguments
)
Io> postOffice messageName := method(call message name)
==> method(
    call message name
)
Io> postOffice messageArgs("one", 2, :three)
==> list("one", 2, : three)
Io> postOffice messageName
==> messageName
```

### 自定义控制结构
实现unless
```
unless := method(
  (call sender doMessage(call message argAt(0))) ifFalse(
  call sender doMessage(call message argAt(1))) ifTrue(
  call sender doMessage(call message argAt(2)))
)

Io> unless(1 == 2, write("one"), write("two"))
one==> false
```
unless先执行第1个参数，如果是false，那么执行第2个参数，否则
执行第3个参数。  
这里doMessage可以执行任意消息，Io会对消息参数进行解释，
但是是延迟绑定和执行的。  








