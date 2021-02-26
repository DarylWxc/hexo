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
## 3. 作用域
## 4. 闭包
## 5. 变量提升
## 6. this的指向
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