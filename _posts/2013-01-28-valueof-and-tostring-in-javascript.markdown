---
layout: post
title: JavaScript 中valueOf() 和 toString()的区别"
date: 2013-01-28 21:24
comments: true
categories: js
---

下面是问题:

```javascript
var x = {
  toString: function() { return "foo"; },
  valueOf: function() { return 42; }
};
window.console.log ("x="+x);
window.console.log ("x="+x.toString());
```
问控制台会输出什么.

这个肯定不能随便猜,作为编程语言,都是有个规范来参考,对于js来说,
规范就是那个Ecma文档,这里我们参考Ecma-262.pdf.

首先在11.6.1,解释了+号的计算流程,我就照抄过来了:
>
The addition operator either performs string concatenation or numeric addition.  
The production AdditiveExpression : AdditiveExpression + MultiplicativeExpression is evaluated as follows:  
1. Let lref be the result of evaluating AdditiveExpression.  
2. Let lval be GetValue(lref).  
3. Let rref be the result of evaluating MultiplicativeExpression.  
4. Let rval be GetValue(rref).  
5. Let lprim be ToPrimitive(lval).  
6. Let rprim be ToPrimitive(rval).  
7. If Type(lprim) is String or Type(rprim) is String, then  
  a. Return the String that is the result of concatenating ToString(lprim) followed by ToString(rprim)  
8. Return the result of applying the addition operation to ToNumber(lprim) and ToNumber(rprim). See the  
Note below 11.6.3.  
NOTE 1 No hint is provided in the calls to ToPrimitive in steps 5 and 6. All native ECMAScript objects except Date objects handle the absence of a hint as if the hint Number were given; Date objects handle the absence of a hint as if the hint String were given. Host objects may handle the absence of a hint in some other manner.  
NOTE 2 Step 7 differs from step 3 of the comparison algorithm for the relational operators (11.8.5), by using the logical-or operation instead of the logical-and operation.  

简单翻译如下:  
+号操作符会进行字符串拼接操作或2个数字相加  
a = b + c会按照如下步骤进行:  
1 计算b的值,赋给lref  
2 计算GetValue(lref), 赋给lval  
3 计算c的值,赋给rref  
4 计算GetValue(rref), 赋给rval  
5 计算ToPrimitive(lval), 赋给lprim  
6 计算ToPrimitive(rval), 赋给rprim  
7 如果Type(lprim)是个 String或者Type(rprim)是个String  
  那么把ToString(rprim)拼接在ToString(lprim)的后面, 作为结果返回  
8 否则将ToNumber(lprim)和ToNumber(rprim)相加, 参考11.6.3  

太坑爹了,一个+号操作还有这么多步骤,而且每一步都有一个新的API...  
那些API这里只简单介绍一下,详细的内容还请参阅规范..  

GetValue(a) 目录在8.7.1   
如果a不是引用,返回a本身,在这里参数都不是引用,所以其他的就不看了..  

ToString(a) 目录在9.8  
a是Undefine类型,返回"undefined"
a是Null类型,返回"null"
a是Boolean类型,返回"true"如果参数是true,返回"false"如果参数是false
a是String,返回参数本身
a是Number类型,这个巨复杂,参考9.8.1
a是Object类型,hint设置为String,然后调用ToPrimitive,然后把结果作为参数调用ToString

ToNumber(a) 目录在9.3  
a是Undefine类型,返回NaN
a是Null类型,返回+0
a是Boolean类型,返回1如果参数是true,返回+0如果参数是false
a是Number类型,返回本身
a是Object类型,hint设置为Number,然后调用ToPrimitive,然后把结果作为参数调用ToNumber

Type() 目录在8  
ECMAScript语言的types是Undefined,Null,Boolean,String,Number和Object.  
Type(x) 是"the type of x"的简写,这里的type指向的ECMAScript语言和规范里定义的那些type.  
大概呢,上面说的就是


这个ToPrimitive()方法我们要看一下,目录在9.1:
说的是如果传入类型是Undefined, Null, Boolean, Number, String就
返回本身,如果是Object,
`返回Object的default value, 这个default value呢,
是调用object本身的内部方法[[DefaultValue]],传入可选的参数hint, 这个
内部方法[[DefaultValue]]在8.12.8定义.`

擦,继续看8.12.8..  
8.12.8很长,这里简单说一下,更详细的请自己参考规范..  
调用内部方法[[DefaultValue]],是如果传递过来的hint是String,如果对象的
toString是个方法,那么调用toString方法,如果结果是个类型为primitive的值,
那么返回这个值;否则如果对象的valueOf是个方法,那么调用ValueOf方法,检查
返回值是否是primitive类型的,如果是则返回;否则,抛出TypeError异常.  
如果传递进来的hint是Number,那么步骤和上面的类似,但是优先调用ValueOf方法
而不是toString方法,都要检查返回值是否是primitive类型.  
然后后面又有解释,说如果调用[[DefaultValue]]时没有传递hint,那么它的行为
就和传递的hint是Number时类似,但是当对象是Date类型时除外,在那种情况下
hint是String.  
然后后面又有解释,说native objects只能返回primitive值,如果宿主对象实现它
自己的[[DefaultValue]]方法,那么它必须保证它的[[DefaultValue]]方法也只会返回
primitive值.  

那什么是primitive呢..  
在4.2里,有这么一句话,`A primitive value is a member of one of the following
build-in types: Undefined, Null, Boolean, Number, and String.`
也就是说,除了Object类型的值,其他的值都认为是primitive的值.  

看了这么多规范,那可以解答上面的问题了.

```javascript
var x = {
  toString: function() { return "foo"; },
  valueOf: function() { return 42; }
};
window.console.log ("x="+x);
window.console.log ("x="+x.toString());
```

"x=" + x




