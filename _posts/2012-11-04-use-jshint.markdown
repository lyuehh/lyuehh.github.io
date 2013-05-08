---
layout: post
title: 使用jshint校验javascript文件
date: 2012-11-04 17:12
comments: true
categories: program
---


## 简介
jshint和[csshint](http://csslint.net/)类似，只是前者是校验js文件的,下面是jshint的校验参数的简单介绍。

## 使用
建议安装node版本的，

```
$ npm install -g
```
然后

```
$ jshint jquery.js
```
即可。
## Options
### (以下内容是从http://www.jshint.com/docs/翻译过来的,以原文为准)
JShint中的校验有2种,一种是强制模式,一种是放松模式.强制模式是让校验更加严格,
而放松模式是为了忽略某些警告.这样做可能会引起困惑,那么只需要记住一点:将强制模式
的选项设置为true表示显示此警告,而将放松模式设置为true表示忽略此警告.

### 强制选项
以下选项设置为true或指定的值,则会在校验时显示此警告(默认不显示警告).

<table class="options table table-bordered table-striped"><tbody><tr>
    <td id="bitwise" class="name">bitwise</td>
    <td class="desc"><p>JavaScript中很少使用位操作符,而且容易和&&混淆</p></td>
  </tr>
  <tr>
    <td id="camelcase" class="name">camelcase</td>
    <td class="desc"><p>强制变量名使用驼峰式风格或者大写字母加下划线风格</p></td>
  </tr>
  <tr>
  <td id="curly" class="name">curly</td>
  <td class="desc"><p>总是把条件或者循环写在大括号里</p></td>
  </tr>
    <tr>
      <td id="eqeqeq" class="name">eqeqeq</td>
      <td class="desc"><p>总是使用===和!==，而不是==和!=</p></td>
    </tr>
    <tr>
      <td id="forin" class="name">forin</td>
      <td class="desc"><p>在for in循环里，必须使用hasOwnProperties过滤元素</p>
      </td>
    </tr>
    <tr>
      <td id="immed" class="name">immed</td>
      <td class="desc"><p>使用立即执行的函数时不要把他们包在括号里</p></td>
    </tr>
    <tr>
      <td id="indent" class="name">indent</td>
      <td class="desc"><p>制定代码的缩进宽度 /* jshint indent:4 */</p>
      </tr>
      <tr>
        <td id="latedef" class="name">latedef</td>
        <td class="desc"><p>变量应该先定义，再使用</p>
        </td>
      </tr>
      <tr>
        <td id="newcap" class="name">newcap</td>
        <td class="desc"><p>构造函数的名称应该以大写字母开头</p>
        </td>
      </tr>
      <tr>
        <td id="noarg" class="name">noarg</td>
        <td class="desc"><p>禁止使用arguments.caller和argument.callee</p></td>
      </tr>
      <tr>
        <td id="noempty" class="name">noempty</td>
        <td class="desc"><p>不要使用空代码块</p></td>
      </tr>
      <tr>
        <td id="nonew" class="name">nonew</td>
        <td class="desc"><p>使用构造函数的副作用，比如new xxx();,不把它赋值给一个变量</p>
        </td>
      </tr>
      <tr>
        <td id="plusplus" class="name">plusplus</td>
        <td class="desc"><p>不建议使用++和--</p></td>
      </tr>
      <tr>
        <td id="quotmark" class="name">quotmark</td>
        <td class="desc"><p>引号的风格，true表示不要求一致性，singie表示只使用单引号，double表示只使用双引号</p></td>
      </tr>
      <tr>
        <td id="undef" class="name">undef</td>
        <td class="desc"><p>禁止使用不声明的变量</p></td>
      </tr>
      <tr>
        <td id="unused" class="name">unused</td>
        <td class="desc"><p>禁止声明变量但不使用</p></td>
      </tr>
      <tr>
        <td id="strict" class="name">strict</td>
        <td class="desc"><p>要求代码运行于Strict mode</p></td>
      </tr>
      <tr>
        <td id="trailing" class="name">trailing</td>
        <td class="desc"><p>禁止代码行最后留有空格</p>
      </tr>
      <tr>
        <td id="maxparams" class="name">maxparams</td>
        <td class="desc"><p>设置函数最多允许的参数个数 /* jshint maxparams:3 */</p>
      </tr>
      <tr>
        <td id="maxdepth" class="name">maxdepth</td>
        <td class="desc"><p>设置大括号最大的嵌套次数 /* jshint maxdepth:2 */</p>
      </tr>
      <tr>
        <td id="maxstatements" class="name">maxstatements</td>
        <td class="desc"><p>设置每个函数允许的最多语句</p>
      </tr>
      <tr>
        <td id="maxcomplexity" class="name">maxcomplexity</td>
        <td class="desc"><p><a href="http://en.wikipedia.org/wiki/Cyclomatic_complexity">参考这里</a></p></td>
      </tr>
      <tr>
        <td id="maxlen" class="name">maxlen</td>
        <td class="desc"><p>设置每行代码最大长度</p></td>
      </tr>
  </tbody></table>

### 可选选项
以下选项设置为true表示忽略此警告(默认显示警告).

<table class="options table table-bordered table-striped"><tbody><tr>
    <td id="asi" class="name">asi</td>
    <td class="desc"><p>是否要求行尾写分号</p></td>
  </tr>
  <tr>
    <td id="boss" class="name">boss</td>
    <td class="desc"><p>是否允许在比较时出现赋值语句</p></td>
  </tr>
  <tr>
    <td id="debug" class="name">debug</td>
    <td class="desc"><p>是否允许出现<code>debugger</code></p></td>
  </tr>
  <tr>
    <td id="eqnull" class="name">eqnull</td>
    <td class="desc"><p>是否允许<code>== null</code>语句</p></td>
  </tr>
  <tr>
    <td id="es5" class="name">es5</td>
    <td class="desc"><p>是否允许使用es5的新特性</p></td>
  </tr>
  <tr>
    <td id="esnext" class="name">esnext</td>
    <td class="desc"><p>是否允许使用ES.next的新特性</p></td>
  </tr>
  <tr>
    <td id="evil" class="name">evil</td>
    <td class="desc"><p>是否允许出现evil</p></td>
  </tr>
  <tr>
    <td id="expr" class="name">expr</td>
    <td class="desc"><p>期望出现赋值语句或函数调用时，出现表达式是否警告</p></td>
  </tr>
  <tr>
    <td id="funcscope" class="name">funcscope</td>
    <td class="desc"><p>是否允许在流程控制里声明变量</p></td>
    </tr>
    <tr>
      <td id="globalstrict" class="name">globalstrict</td>
      <td class="desc"><p>是否允许使用global strict mode</p></td>
    </tr>
    <tr>
      <td id="iterator" class="name">iterator</td>
      <td class="desc"><p>是否允许使用__iterator__属性</p></td>
    </tr>
    <tr>
      <td id="lastsemic" class="name">lastsemic</td>
      <td class="desc"><p>是否允许遗失最后的分号</p></td>
    </tr>
    <tr>
      <td id="laxbreak" class="name">laxbreak</td>
      <td class="desc"><p>是否允许不安全的断行</p></td>
    </tr>
    <tr>
      <td id="laxcomma" class="name">laxcomma</td>
      <td class="desc"><p>是否允许object中的属性逗号前置风格</p></td>
    </tr>
    <tr>
      <td id="loopfunc" class="name">loopfunc</td>
      <td class="desc"><p>是否允许在循环里使用函数</p></td>
    </tr>
    <tr>
      <td id="multistr" class="name">multistr</td>
      <td class="desc"><p>是否允许多行字符串</p></td>
    </tr>
    <tr>
      <td id="proto" class="name">proto</td>
      <td class="desc"><p>是否允许使用__proto__属性</p></td>
    </tr>
    <tr>
      <td id="scripturl" class="name">scripturl</td>
      <td class="desc"><p>是否允许url里出现script,比如javascript:...</p></td>
    </tr>
    <tr>
      <td id="smarttabs" class="name">smarttabs</td>
      <td class="desc"><p>是否允许tab和空格混用</p></td>
    </tr>
    <tr>
      <td id="shadow" class="name">shadow</td>
      <td class="desc"><p>是否允许声明其他地方已经声明过的变量</p></td>
    </tr>
    <tr>
      <td id="sub" class="name">sub</td>
      <td class="desc"><p>建议使用persion.name而不是persion['name']</p></td>
    </tr>
    <tr>
      <td id="supernew" class="name">supernew</td>
      <td class="desc"><p>是否允许使用诡异的构造器比如new function() { … }和new Object</p></td>
    </tr>
    <tr>
        <td id="validthis" class="name">validthis</td>
        <td class="desc"><p>是否允许在strict mode的非构造函数中使用this</p></td>
    </tr>
  </tbody></table>

### 环境
以下选项打开表示是否是运行在所指的环境下.

<table class="options table table-bordered table-striped"><tbody><tr>
    <td id="browser" class="name">browser</td>
    <td class="desc"><p>是否是浏览器环境</p></td>
  </tr>
  <tr>
    <td id="couch" class="name">couch</td>
    <td class="desc"><p>是否是CouchDB环境</p></td>
  </tr>
  <tr>
    <td id="devel" class="name">devel</td>
    <td class="desc"><p>是否是开发环境</p></td>
  </tr>
  <tr>
    <td id="dojo" class="name">dojo</td>
    <td class="desc"><p>是否使用dojo</p></td>
  </tr>
  <tr>
    <td id="jquery" class="name">jquery</td>
    <td class="desc"><p>是否使用jQuery</p></td>
  </tr>
  <tr>
    <td id="mootools" class="name">mootools</td>
    <td class="desc"><p>是否使用mootools</p></td>
  </tr>
  <tr>
    <td id="node" class="name">node</td>
    <td class="desc"><p>是否是node环境</p></td>
  </tr>
  <tr>
    <td id="nonstandard" class="name">nonstandard</td>
    <td class="desc"><p>是否使用非标准方法，比如escape和unescape</p></td>
  </tr>
  <tr>
    <td id="prototypejs" class="name">prototypejs</td>
    <td class="desc"><p>是否使用Prototyps</p></td>
  </tr>
  <tr>
    <td id="rhino" class="name">rhino</td>
    <td class="desc"><p>是否是Rhino环境</p></td>
  </tr>
  <tr>
    <td id="worker" class="name">worker</td>
    <td class="desc"><p>是否使用Web Worker</p></td>
  </tr>
  <tr>
    <td id="wsh" class="name">wsh</td>
    <td class="desc"><p>是否是Windows Script Host环境</p></td>
  </tr>
  <tr>
    <td id="yui" class="name">yui</td>
    <td class="desc"><p>yui 是否使用yui</p></td>
</tr></tbody></table>

### Legacy
<table class="options table table-bordered table-striped"><tbody><tr>
    <td id="nomen" class="name">nomen</td>
    <td class="desc"><p>是否禁止使用_下划线变量</p></td>
  </tr>
  <tr>
    <td id="onevar" class="name">onevar</td>
    <td class="desc"><p>是否只允许使用一个var</p></td>
    </tr>
    <tr>
      <td id="passfail" class="name">passfail</td>
      <td class="desc"><p>是否第1个错误出处中断</p></td>
    </tr>
    <tr>
      <td id="white" class="name">white</td>
      <td class="desc"><p>强制要求严格的空白</p></td>
  </tr></tbody>
</table>

