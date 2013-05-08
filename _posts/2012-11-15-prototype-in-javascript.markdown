---
layout: post
title: Javascript中的prototype简介
date: 2012-11-15 22:58
comments: true
categories: javascript
---

JavaScript中的对象不像C++、SmallTalk一样是由类产生的，它通过字面量或者构造器创建，每个构造器都是一个函数，每个函数都有一个属性叫做prototype，它用于实现基于原型的继承，也可以用来共享属性。对象可以通过new 构造器 的方式创建，比如，new Date(2009, 11)创建了一个日期对象，不使用new 关键字调用构造器时产生的结果取决于构造器本身，例如Date()会生成一个代表当前时间的字符串而不是产生一个Date对象。  

每一个通过构造器创建的对象都暗含一个引用(成为对象的原型)，指向构造器的prototype属性，而且，对象的原型也可能指向一个非null的原型，等等；这叫做原型链。当有一个引用指向一个对象的属性，那么它会指向这个对象的原型链中第1个拥有那个属性的属性值。也就是说，当访问对象的一个属性时，首先检查那个对象，如果它包含那个属性，那么就会指向它，如果它不包含，就会检查那个对象的原型，看那个值是否存在，如果不存在，继续检查那个对象的原型的原型，等等。
在基于类的面向对象语言中，一般，状态是包含在实例中的，方法是包含在类中的，继承只是结构和行为，在JavaScript中，状态和方法都是包含在对象中的，结构、行为、状态都是继承的。  
以上内容翻译自ecma-262.pdf 4.2.1，翻译的太差，见笑了。。

# 继承

prototype在javaScript中主要用于继承，一步一步来：  

## 1

首先声明Animal构造函数：

```javascript
function Animal(name) {
   this.name = name;
}
Animal.prototype.say = function() {
   console.log('Name: ' + this.name);
};
```

然后声明Cat构造函数：

```javascript
function Cat(name) {
   this.name = name;
}
Cat.prototype = new Animal();
var c1 = new Cat('cat 1');
```

这样c1就会继承Animal的say方法了，但是这样`Cat.prototype.constructor`就不指向构造器本身，而是指向Animal了，所以我们需要重写`Cat.prototype.constructor`;

## 2

```javascript
function Cat(name) {
   this.name = name;
}
Cat.prototype = new Animal();
Cat.prototype.constructor = Cat;
var c1 = new Cat('cat 1');
```

这里Cat.prototype指向了一个新的Animal对象，所以也继承了Animal的实例属性和原型属性，我们一般只需要继承实例属性即可。

## 3

```javascript
function Cat(name) {
   this.name = name;
}
Cat.prototype = Animal.prototype;
Cat.prototype.constructor = Cat;
var c1 = new Cat('cat 1');
```

但是这里有一个问题，子类Cat的原型指向父类的原型，他们是引用传递的，当我们修改了子类原型上的方法，父类也会受到影响，这不是我们希望的，所以我们需要一个代理对象来隔离他们。

```javascript
function Cat(name) {
   this.name = name;
}
function F() {};
F.prototype = Animal.prototype;
Cat.prototype = new F();
Cat.prototype.constructor = Cat;
var c1 = new Cat('cat 1');
```

把上面的方法封装一下：

```javascript
var extend = function(Child, Parent) {
   function F() {};
   F.prototype = Parent.prototype;
   Child.prototype = new F();
   Child.prototype.constructor = Child;
};
extend(Cat, Animal);
```

## 4

有时候我们需要从子类调用父类的方法，所以我们在子类上设置一个属性指向父类。

```javascript
var extend = function(Child, Parent) {
   function F() {};
   F.prototype = Parent.prototype;
   Child.prototype = new F();
   Child.prototype.constructor = Child;
   Child.__super__ = Parent.prototype;
};
```

## 5

JavaScript还可以使用其他方式的继承，比如直接把父类的属性复制到子类中去。

```javascript
var extend2 = function(Child, Parent) {
   var p = Parent.prototype;
     var c = Child.prototype;
     for (var i in p) {
          c[i] = p[i];
     }
     c.__super__ = p;
}
```

## 6

其实Parent.prototype和Child.prototype本质上都是对象，所以上面的可以简写为：

```javascript
var extend3 = function(o) {
     var c = {};
     for(var i in p) {
          c[i] = p[i];
     }
     c.__super__ = p;
     return c;
}
```

## 7

前面复制父类属性时，如果某个属性是引用类型，比如是对象或者数组，那么复制以后，修改子类的属性，也会影响到父类。
比如：
```javascript
function A(name) {
  this.name = name;
}
A.prototype.a = [1,2,3];

var a1 = new A('a');
var b1 = copy(a1);
b1.name = 'b';

console.log(b1.name + ' ' + b1.a); // b 1,2,3
console.log(a1.name + ' ' + a1.a); // a 1,2,3

b1.prototype = A.prototype;
b1.prototype.a = [4,5,6];

console.log(b1.name + ' ' + b1.a); // b 4,5,6
console.log(a1.name + ' ' + a1.a); // b 4,5,6

```

所以这里需要深度拷贝。

```javascript
function deepCopy(p, c) {
    var c = c || {};
    for (var i in p) {
        if (typeof p[i] === 'object') {
            c[i] = (p[i].constructor === Array) ? [] : {};
            deepCopy(p[i], c[i]);
        } else {
            c[i] = p[i];
        }
    }
    return c;
}
```

## 8

前面我们使用了属性拷贝和原型继承来实现继承，其实我们可以把他们结合起来。
这里拷贝的是父类的静态成员，类似于Java中的类变量。  

```javascript
var extend = function (Child, Parent) {
  for (var i in Parent) {
    if(Parent.hasOwnProperty(i)) {
      Child[i] = Parent[i];
    }
  }
  function F() {};
  F.prototype = Parent.prototype;
  Child.prototype = new F();
  Child.prototype.constructor = Child;
  Child.__super__ = Parent.prototype;
};
```

## 9

在JavaScript里继承的实现方法很多，比如还可以借用父类的构造器来进行继承，这里就不再介绍了。大家可以参考其他资料。

## 10

CoffeeScript中的继承，如下是官网上的例子：

```coffeescript
class Animal
  constructor: (@name) ->
  move: (meters) ->
    alert @name + " moved #{meters}m."

class Snake extends Animal
  move: ->
    alert "Slithering..."
    super 5

class Horse extends Animal
  move: ->
    alert "Galloping..."
    super 45

sam = new Snake "Sammy the Python"
tom = new Horse "Tommy the Palomino"
sam.move()
tom.move()
```

编译成JavaScript后是这样：

```javascript
__hasProp = {}.hasOwnProperty,
__extends = function(child, parent) {
  for (var key in parent) {
    if (__hasProp.call(parent, key))
      child[key] = parent[key];
  }
  function ctor() {
    this.constructor = child;
  }
  ctor.prototype = parent.prototype;
  child.prototype = new ctor();
  child.__super__ = parent.prototype;
  return child;
};
Animal = (function() {
  function Animal(name) {
    this.name = name;
  }
  Animal.prototype.move = function(meters) {
    return alert(this.name + (" moved " + meters + "m."));
  };
  return Animal;
})();
Snake = (function(_super) {
  __extends(Snake, _super);
  function Snake() {
    return Snake.__super__.constructor.apply(this, arguments);
  }
  Snake.prototype.move = function() {
    alert("Slithering...");
    return Snake.__super__.move.call(this, 5);
  };
  return Snake;
})(Animal);
Horse = (function(_super) {
  __extends(Horse, _super);
  function Horse() {
    return Horse.__super__.constructor.apply(this, arguments);
  }
  Horse.prototype.move = function() {
    alert("Galloping...");
    return Horse.__super__.move.call(this, 45);
  };
  return Horse;
})(Animal);
sam = new Snake("Sammy the Python");
tom = new Horse("Tommy the Palomino");
sam.move();
tom.move();
```

里面的__extend函数和上面介绍的类似，就是用来实现继承。  


### reference

* <http://www.zipeng.info/archives/javascript-inheritance.html>
* <http://ioio.name/object-oriented-javascript-note.html>
* <http://island205.github.com/2012/04/01/oop.html>
* <http://ruby-china.org/topics/4789>
* <http://jashkenas.github.com/coffee-script/>
