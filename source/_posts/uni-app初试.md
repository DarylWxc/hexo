---
title: uni-app初试
date: 2021-03-31 09:14:10
tags:
 - 移动端开发
 - Vue
categories: 移动端
---
### 1. 文档查阅
初始化hello-uniapp项目，查看项目相关文件，src为主要文件夹
common：文件夹为一些配置插件封装
components：组件目录
hybrid：存放本地HTML文件
platforms：存放各平台专用页面文件
pages：业务页面文件存放目录
static：存放本地静态资源
wxcomponents：存放小程序组件
manifest.json：配置应用名称、appid、logo、版本等打包信息
pages.json：配置页面路由、导航条、选项卡等页面类信息

## 1.1 写法
标签与小程序相似
page相当于body节点
```
page{
   background:#ccc;
}
```
### 2. 疑难杂症
1.引入iconfont方式，添加图标到创建的项目文件夹中，然后Unicode选项生成代码，直接讲代码复制到新建的css文件中，然后在app.vue文件引入该CSS文件。使用时:
```
style:iconfont{
   font-family:"iconfont" //之前css文件里的font-family值
   font-size:16rpx; //等
}
<text class="iconfont">{复制的图标代码}</text>//class为定义的iconfont
```
添加新图标只需要生成新代码复制到css文件中即可
2.使用uview组件库，搜索框，input输入框无法设置宽度
套一层view设置宽度即可 //反应失灵
