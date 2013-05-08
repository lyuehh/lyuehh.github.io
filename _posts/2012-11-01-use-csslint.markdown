---
layout: post
title: 使用csslint校验css文件
date: 2012-11-01 22:55
comments: true
categories: program
---

# 简介
CSS Lint是一个开源的校验CSS文件质量的工具，最初是由[Nicholas C. Zakas](http://www.nczonline.net/)和[Nicole Sullivan](http://www.stubbornella.org/)编写的，最初版本在Velocity会议上于2011年6月发布。

它静态的分析源代码，根据一定的规则，为开发者找出其中可能会出错或者引发问题的地方。

以下是规则的翻译，有删减，请以原文为准。

# 规则
## 1. 可能的错误
### 1.1 Beware of box model size - 注意盒模型

```
.mybox {
    border: 1px solid black;
    padding: 5px;
    width: 100px;
}
```
会给出警告，mybox实际上的宽是112px,
大部分浏览器下你使用box-sizing会使mybox的宽为100px

```
.mybox {
    box-sizing: border-box;
    border: 1px solid black;
    padding: 5px;
    width: 100px;
}
```

### 1.2 Require properties appropriate for display - display 应该有合适的属性  

```
display: inline, the width,height, margin-top, margin-bottom,float
```  

对inline元素无效  

```
margin-left,margin-right
```

依然有效  

```
display: inline used with width, height, margin, margin-top, margin-bottom, and float.  
display: inline-block used with float.  
display: block used with vertical-align.  
display: table-* used with margin (and all variants) or float.
```

### 1.3 Disallow duplicate properties - 重复的属性

```
.mybox {
    width: 100px;
    width: 120px;
}
```

### 1.4 Disallow empty rules - 禁止空属性

```
.foo {
}
```

### 1.5 Require use of known properties - 只允许使用已知的属性

```
a {
    clr: red;
}
```

## 2. 兼容性
### 2.1 Disallow adjoining classes - 禁用连续的css选择器

```
.foo.bar {
    border: 1px solid black;
}
.first .abc.def {
    color: red;
}
```

### 2.2 Disallow box-sizing - 禁用box-sizing,ie 6,7 不支持此属性

```
.mybox {
    box-sizing: border-box;
    border: 1px solid black;
    padding: 5px;
    width: 100px;
}
```

### 2.3 Require compatible vendor prefixes - 使用兼容的浏览器自定义前缀

```
/* Missing -moz, -ms, and -o */
.mybox {
    -webkit-transform: translate(50px, 100px);
}
/* Missing -webkit */
.mybox {
    -moz-border-radius: 5px;
}
```

### 2.4 Require all gradient definitions - 声明所有的css渐变

```
/* Missing -moz, -ms, and -o */
.mybox {
    background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#1e5799), color-stop(100%,#7db9e8));
    background: -webkit-linear-gradient(top,  #1e5799 0%,#7db9e8 100%);
}
/* Missing old and new -webkit */
.mybox {
    background: -moz-linear-gradient(top,  #1e5799 0%, #7db9e8 100%); 
    background: -o-linear-gradient(top,  #1e5799 0%,#7db9e8 100%);
    background: -ms-linear-gradient(top,  #1e5799 0%,#7db9e8 100%);
}
```

### 2.5 Disallow negative text-indent - 禁用为负值的text-indent ,建议加上direction

```
.mybox {
    background: url(bg.png) no-repeat;
    direction: ltr;
    text-indent: -9999px;
}
```

### 2.6 Require standard property with vendor prefix - 使用标准的浏览器前缀

```
/* missing standard property */
.mybox {
    -moz-border-radius: 5px;
}
/* standard property should come after vendor-prefixed property */
.mybox {
    border-radius: 5px;
    -webkit-border-radius: 5px;
}
```

### 2.7 Require fallback colors - 使用向后兼容的raga颜色

```
/* missing fallback color */
.mybox {
    color: rgba(100, 200, 100, 0.5);
}
/* fallback color should be before */
.mybox {
    background-color: hsl(100, 50%, 100%);
    background-color: green;
}
```

### 2.8 Disallow star hack (new in v0.9.8) - 禁用ie 6 7 的*号hack

```
.mybox {
    border: 1px solid black;
    *width: 100px;
}
```

### 2.9 Disallow underscore hack (new in v0.9.8) - 禁用ie 6的下划线_ hack

```
.mybox {
    border: 1px solid black;
    _width: 100px;
}
```

## 3. 性能
### 3.1 Don't use too many web fonts - 不允许使用过多的web fonts

### 3.2 Disallow @import - 禁用@import 因为要阻塞下载

### 3.3 Disallow selectors that look like regular expressions - 禁用类似正则表达式的选择器，可能会影响性能
禁用

 ```*=, |=, ^=, $=, or ~=.```

```
.mybox[class~=xxx]{
    color: red;
}
.mybox[class^=xxx]{
    color: red;
}
.mybox[class|=xxx]{
    color: red;
}
.mybox[class$=xxx]{
    color: red;
}
.mybox[class*=xxx]{
    color: red;
}
```

这些允许使用

```
.mybox[class=xxx]{
    color: red;
}
.mybox[class]{
    color: red;
}
```

### 3.4 Disallow universal selector - 禁用星号选择器，可能会有性能问题

```
* {
    color: red;
}
.selected * {
    color: red;
}
```

这些是允许的

```
/* universal selector is not key */
.selected * a {
    color: red;
}
```

### 3.5 Disallow unqualified attribute selectors - 禁用不合适的属性选择器

```
.mybox [type=text] {
    background: #fff;
    color: #000;
    background: rgba(255, 255, 255, 0.5);
}
```

浏览器从右往左解析，会先匹配所有的元素，然后检查attribute
这些是允许的

```
/* unqualified attribute selector is not key */
.selected [type=text] a {
    color: red;
}
```

### 3.6 Disallow units for zero values - 当值为0是不必写单位
没有必要，还可以省字节

### 3.7 Disallow overqualified elements - 不需要写没必要的元素
```
div.mybox {
    color: red;   
}
.mybox li.active {
    background: red;
}
```

这些允许的

```
/* Two different elements in different rules with the same class */
li.active {
    color: red;
}
p.active {
    color: green;
}
```

### 3.8 Require shorthand properties - 要求使用简写

```
.mybox {
    margin-left: 10px;
    margin-right: 10px;
    margin-top: 20px;
    margin-bottom: 30xp
}
```

如果只有2个，则允许，如

```
.mybox {
    margin-left: 10px;
    margin-right: 10px;
}
```

### 3.9 Disallow duplicate background images - 禁止重复的background image
如

```
/* multiple instances of the same URL */
.heart-icon {
    background: url(sprite.png) -16px 0 no-repeat;
}
.task-icon {
    background: url(sprite.png) -32px 0 no-repeat;
}
```

建议使用

```
/* fallback color before newer format */
.icons {
    background: url(sprite.png) no-repeat;
}
.heart-icon {
    background-position: -16px 0;
}
.task-icon {
    background-position: -32px 0;
}
```

## 4. 可维护性
### 4.1 Disallow too many floats - 禁止float超过10个

### 4.2 Don't use too many font-size declarations - 禁止过多的font-size声明，不允许超过10个

### 4.3 Disallow IDs in selectors - 为了提高代码重用，禁止使用id选择器

### 4.4 Disallow !important - 禁用!importtant

## 5. 提高可用性
### 5.1 Disallow outline:none - 禁用 outline：none，某些用户需要outline来确定焦点

```
/* no :focus */
a {
    outline: none;
}
/* no :focus */
a {
    outline: 0;
}
/* :focus but missing a replacement treatment */
a:focus {
    outline: 0;
}
```

这些是可以的

```
/* :focus with outline: 0 and provides replacement treatment */
a:focus {
    border: 1px solid red;
    outline: 0;
}
```

## 6. 其他准则
### 6.1 Disallow qualified headings - 禁止指定特定的h1 ~ h6

```
/* qualified heading */
.box h3 {
    font-weight: normal;
}
/* qualified heading */
.item:hover h3 {
    font-weight: bold;
}
```

这样写是可以的

```
/* Not qualified */
h3 {
    font-weight: normal;
}
```

### 6.2 Headings should only be defined once - h1 ~ h6应该只定义1次
禁止这些

```
/* Two rules for h3 */
h3 {
    font-weight: normal;
}
.box h3 {
    font-weight: bold;
}
```

这些是可以的

```
/* :hover doesn't count */
h3 {
    font-weight: normal;
}
h3:hover {
    font-weight: bold;
}
```

### reference

* <https://github.com/stubbornella/csslint/wiki>
























