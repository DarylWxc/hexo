---
title: Vue响应式原理
date: 2021-03-15 10:56:14
tags:
 - 前端框架
 - Vue
categories: Web前端
---
## 1. 数据初始化
Vue源码中在initState中进行了数据初始化，为数据添加响应式。针对props，methods，data，computed和watch，做数据的初始化处理，响应式转换。
## 2. initProps
Props用于父子组件间传值(父传子)。
:test=test会被解析成{attrs: {test: test}}，并作为子组件的render函数。
创建VNode遇到child占位符时，根据attrs属性进行规范校验，最后以propsData形式传入Vnode构造器中。
通过proxy为props做了一层代理，可通过vue实例代理访问到props的值，本质上是利用Object.defineProperty对数据的getter和setter方法进行重写。
总结：props以propsData的形式在Vnode的属性存在，通过proxy进行代理，然后实例访问。
## 3. initMethods
methods方法定义必须是函数，命名不能与props重复。定义的方法都将挂载在根实例上。
## 4. initData
核心方法是observe，在observe方法中将数据对象标记为响应式对象，然后进行响应式处理。同props，通过proxy对data做一层处理，可通过实例访问对象属性。
## 5. initComputed
1.computed可以是对象，也可以是函数，函数必须有getter。
2.针对每个computed属性都需要创建一个监听的依赖(watcher)。
computed的命名防止与props，data冲突
## 6. 响应式系统
observe：挂载组件，引入observe类，通过Object.defineProperty，对数据的getter和setter进行改写，读取getter进行依赖手机，在setter时进行依赖更新。
watcher：一个watcher实例急速一个依赖，watcher记录这个依赖监听的状态以及如何更新操作的方法。渲染数据到真实DOM时会创建watcher。
## 7. 小结
最终都是调用Object.defineProperty进行数据拦截。



