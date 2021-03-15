---
title: JavaScript基础
date: 2021-02-26 15:17:21
tags:
 - JavaScript
categories: web前端
---
## 1. 原型链
每个函数都有prototype，指向了一个对象，该对象为实例的原型。
每个JS对象（除了null）都具有_proto_属性，指向该对象的原型。
每个原型都具有constructor属性，指向关联的构造函数。
Object.prototype._proto_为null代表该对象没有原型。
## 2. 继承
 - 原型链继承
```
function Parent () {
    this.name = 'kevin';
}

Parent.prototype.getName = function () {
    console.log(this.name);
}

function Child () {

}

Child.prototype = new Parent();

var child1 = new Child();

console.log(child1.getName()) // kevin

var child1 = new Child(); // 引用类型的属性被所有实例共享

child1.names.push('yayu'); 

console.log(child1.names); // ["kevin", "daisy", "yayu"]

var child2 = new Child(); // 创建child实例时无法向Parent传参

console.log(child2.names); // ["kevin", "daisy", "yayu"]
```
 - 借用构造函数（经典继承）
```
function Parent () {
    this.names = ['kevin', 'daisy'];
}

function Child () {
    Parent.call(this);
}

var child1 = new Child();

child1.names.push('yayu');

console.log(child1.names); // ["kevin", "daisy", "yayu"]

var child2 = new Child();

console.log(child2.names); // ["kevin", "daisy"]

function Parent (name) {
    this.name = name;
}

function Child (name) {
    Parent.call(this, name);
}

var child1 = new Child('kevin');

console.log(child1.name); // kevin

var child2 = new Child('daisy');

console.log(child2.name); // daisy
```
优点：
1.避免了引用类型的属性被所有实例共享
2.可以在Child中向Parent传参
缺点：
方法都在构造函数中定义，每次创建实例都会创建一遍方法。
 - 组合继承
原型链继承和经典继承合并。
```
function Parent (name) {
    this.name = name;
    this.colors = ['red', 'blue', 'green'];
}

Parent.prototype.getName = function () {
    console.log(this.name)
}

function Child (name, age) {

    Parent.call(this, name);
    
    this.age = age;

}

Child.prototype = new Parent();
Child.prototype.constructor = Child;

var child1 = new Child('kevin', '18');

child1.colors.push('black');

console.log(child1.name); // kevin
console.log(child1.age); // 18
console.log(child1.colors); // ["red", "blue", "green", "black"]

var child2 = new Child('daisy', '20');

console.log(child2.name); // daisy
console.log(child2.age); // 20
console.log(child2.colors); // ["red", "blue", "green"]
```
融合原型链和构造函数的优点，最常用的继承模式。
 - 原型式继承
```
function createObj(o) {
    function F(){}
    F.prototype = o;
    return new F();
}
```
ES5 Object.create的模拟实现，将传入的对象作为创建的对象的原型。
缺点：
包含引用类型的属性值始终会共享相应的值，与原型链继承一样。
 - 寄生式继承
创建一个仅用与封装继承过程的函数，该函数在内部以某种形式来做增强对象，最后返回对象。
```
function createObj (o) {
    var clone = Object.create(o);
    clone.sayName = function () {
        console.log('hi');
    }
    return clone;
}
```
缺点：跟借用构造函数模式一样，每次创建对象都会创建一遍方法。
 - 寄生组合式继承
```
function Child (name, age) {
    Parent.call(this, name);
    this.age = age;
}

// 关键的三步
var F = function () {};

F.prototype = Parent.prototype;

Child.prototype = new F();


var child1 = new Child('kevin', '18');

console.log(child1);
//封装
function object(o) {
    function F() {}
    F.prototype = o;
    return new F();
}

function prototype(child, parent) {
    var prototype = object(parent.prototype);
    prototype.constructor = child;
    child.prototype = prototype;
}

// 当我们使用的时候：
prototype(Child, Parent);
```
普遍认为是最理想的继承范式。
## 3. 作用域
对于每个执行上下文，都有三个重要属性：
 - 变量对象（Variable）
 - 作用域链（Scope）
 - this
全局作用域：
window对象的上下文
块级作用域：
用let声明的代码块{}内
函数作用域：
函数上下文的作用域{}内
作用域链：
不断向上访问，直到全局作用域
## 4. 闭包
理解：引用另一个函数作用域中变量的函数。
闭包可以传入this对象作为参数，通过该对象访问this上下文的值。
由于闭包会保留他们包含函数的作用域，所以使用闭包要注意，内存的回收。
## 5. 变量提升
var声明的变量和方法，都会提升到全局对象上。
全局对象就是由Object构造函数实例化的一个对象。
函数上下文的变量对象初始化只包括Arguments对象
在进入执行上下文时会给变量对象添加形参(arguments)、函数声明(func)、变量声明(var)等初始化的属性值
在代码执行阶段，会再次修改变量对象的属性值
进入执行上下文中，首先会处理函数声明，其次处理变量声明，如果变量名称跟已声明的元素相同，则声明不会干扰已经存在的这类属性。
## 6. this的指向
执行上下文都有this属性
标准函数中，this引用的是把函数当成方法调用的上下值。
箭头函数会保留定义它时的上下文
## 7. 立即执行函数
## 8. instanceof原理
## 9. bind的实现
## 10. apply和call
## 11. 柯里化
## 12. v8垃圾回收机制
## 13. 浮点数精度
## 14. new操作符
## 15. 事件循环机制
## 16. promise原理
## 17. generator原理