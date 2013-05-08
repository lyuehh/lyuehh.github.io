---
layout: post
title: JavaScript学习笔记 - part1
date: 2012-12-17 15:38
comments: true
categories: javascript
---


1. 不要重复自己，代码只写一次，不复制粘贴
2. 缓存数据
3. 使用高阶函数
4. 使用链式操作
5. 使用闭包，隔离变量
6. 使用'use strict'
7. 使用封装
8. 捕获错误

 - - -
## 不要重复

```javascript
/*
  demo1: do not repeat yourself
*/
$.ajax({
  'url': '/user',
  'data': 'dept=aaa&active=true&_=' + Math.random(),
  'dataType': 'json',
  'headers': {
    'X-CSRF-Token': $('#csrf').attr('content');
  },
  'type': 'GET',
  'success': function(ret) {
    if(ret.result === 0) {
      console.log('data: ' + JSON.stringify(ret.data));
    } else {
      console.log('request error: ' + ret.msg);
    }
  },
  'error': functoin(jqXHR, textStatus, errorThrown) {
    console.log('ajax error...')
  }
});
/*
  1. 使用全局ajaxError
*/
$(document).ajaxError(function() {
  console.log('ajax error...')
});
/*
  2. 使用全局ajaxSetup
*/
$.ajaxSetup({
  'dataType': 'json',
  'headers': {
    'X-CSRF-Token': $('#csrf').attr('content');
  },
  'cache': false
});
/*
  3. 使用快捷方法
*/
$.get('/user', function(ret) {
  // ....
});
/*
  4. 统一的错误处理
*/
var showErrorTips = function(ret) {
  console.log('request error: ' + ret.msg)
};
var Ajax = {
    get: function(url, callback) {
      $.get(url, function(ret) {
        if(ret.result === 0) {
          if(ret.data) {
            callback(ret.data);
          } else {
            callback(ret);
          }
        } else {
          showErrorTips(ret);
        }
      });
    },
    post: function(url, data, callback) {
      $.post(url, data, function (ret) {
        if(ret.result === 0) {
          if(ret.data) {
            callback(ret.data);
          } else {
            callback(ret);
          }
        } else {
          showErrorTips(ret);
        }
      });
    }
  };
/*
  result
*/
Ajax.get('/user' + '?dept=aaa&active=true', function(data) {
  console.log('data: ' + JSON.stringify(data));
})
```

## 缓存数据

```javascript
/* tiny_store.js */
function Store() {
  this._data = {};
}
Store.prototype.set = function(key, value) {
  this._data[key] = value;
};
Store.prototype.get = function(key) {
  return this._data[key];
};
Store.prototype.clear = function() {
  this._data = {};
};
```

```javascript
var store = new Store();
Ajax.get('/user', function(data) {
  store.set('user', data);
});
console.log(store.get('user')); // use user anywhere else..
```

## 使用高阶函数

```javascript
/*
* for loop
*/
var sum = function(arr) {
  var sum = 0;
  for(var i=0,l=arr.length; i<l; i++) {
    sum += i;
  }
  return sum;
};
/*
* high level function
*/
var sum2 = function(arr) {
  return arr.reduce(function(s, i) {
    return s + i;
  }, 0);
};
```

## 使用链式操作

```javascript
// use underscore.js, from http://underscorejs.org/#chain
var stooges = [{name : 'curly', age : 25}, {name : 'moe', age : 21}, {name : 'larry', age : 23}];
var youngest = _.chain(stooges)
  .sortBy(function(stooge){ return stooge.age; })
  .map(function(stooge){ return stooge.name + ' is ' + stooge.age; })
  .first()
  .value();
console.log(youngest);
```

## 使用闭包

```javascript
(function(){
  // code here...
}();
```

## 使用'use strict'

```javascript
(function(){
  'use strict';
  // code here...
}();
```

## 使用封装

```javascript
var store = (function() {
  var data;
  var getData = function () {
    return data;
  };
  var setData = function (d) {
    data = d;
  };
  var clearData = function () {
    data = null;
  };
  return {
    getData: getData,
    setData: setData,
    clearData: clearData
  };
})();
```

##  捕获错误
大部分的js方法不会抛异常，比如除以0，访问不存在的属性等，但是也有一些会抛出异常，当抛出异常时，js就不会继续执行，大部分情况下会影响用户继续操作，一下列出部分可能会抛出异常的js方法。  
所以调用这些方法时，一定要小心，可以先校验参数，看是否是需要的类型，也可以加上try catch。

### 数组操作
```javascript
new Array(-1); // invalid array length

[1,2,3,4].reduce(function(x,y) {
 return x*y;
}); // reduce of empty array with no initial value
```

### URL操作
```javascript
decodeURIComponent('%XX'); //malformed URI sequence

// 以下操作也会抛出异常
encodeURI(uri);
decodeURI();
encodeURIComponent();
```

### JSON, evel, function
```javascript

JSON.parse('xx'); // SyntaxError: JSON.parse
eval('asdf'); // ReferenceError: asdf is not defined

new Function('var'); // SyntaxError: missing variable name

_.include.apply([1,2,3],1);
// TypeError: second argument to Function.prototype.apply must be an array
```

### 数字操作
```javascript
var a = 34234234234.2342343;
a.toExponential(333); // RangeError: precision 333 out of range

// 这些操作也会
toFixed()
toPrecision()
```

### 对象操作
```javascript
Object.create('a');
//TypeError: Object prototype may only be an Object or null

// 这些操作也会
Object.defineProperties('a')
Object.defineProperty()
Object.freeze('a')
Object.isExtensible('a')
```
