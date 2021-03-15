---
title: CSS基础
date: 2021-03-15 10:26:23
tags:
 - CSS
 - 响应式布局
categories: 页面样式
---
## 1. 盒模型？
盒模型：框模型，包含content(内容)、padding(内边距)、border(边框)、margin(外边距)。
## 2. IE模型和标准模型的区别？
IE模型：width=content+padding，height=content+padding
标准模型：width=content，height=content
## 3. CSS设置方式
可通过CSS3新增的属性box-sizing设置盒模型的模式，content-box(标准模型)，IE模型(border-box)。
## 4. JavaScript设置盒模型的宽高
1.dom.style.width/height //只能取到行内样式的宽和高，style标签中的link外链取不到。
2.dom.currentStyle.width/height //取到的是最终渲染后的宽高，只IE支持
3.window.getComputedStyle(dom).width/height //同(2)，IE9以上支持，其他浏览器支持
4.dom.getBoundingClientRect().width/height //同(3)，还可取到对于视窗的上下左右的距离
## 5. 外边距重叠
当两个垂直外边距相遇时，会形成外边距，合并后的外边距高度等于两个发生合并的外边距的高度中的较大者。普通文档流才会发生，行内框，浮动框和绝对定位之间的外边距不会合并。
## 6. BFC
BFC：块级格式化上下文
 - BFC元素垂直方向的边距会发生重叠。属于不同BFC外边距不会发生重叠。
 - BFC的区域不会与浮动元素的布局重叠。
 - BFC元素是一个独立的容器，外面的元素不会影响里面的元素。里面的元素也不会影响外面的元素。
 - 计算BFC高度的时候，浮动元素也会参与计算（清楚浮动）。
## 7. 触发条件
 - overflow部位visible；
 - float的值不为none；
 - position的值不为static或relative；
 - display属性为inline-block，table，table-cell，table-caption，flex，inline-flex
当子元素浮动不会影响父元素时，可以给父元素触发BFC。