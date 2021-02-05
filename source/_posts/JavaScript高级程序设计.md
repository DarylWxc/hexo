---
title: JavaScript高级程序设计
date: 2020-11-23 09:43:04
tags:
 - javaScript
categories: javaScript高级程序设计
---
# 1.1 历史回顾
网站数据量大，复杂。需要JS来解决，优化。
# 1.2 JS实现
JS = ECMAScript（核心） + DOM（文档对象模型） + BOM（浏览器对象模型）
## 1.2.1（ECMAScript）
ES：网页提供ES的基准实现和与环境自身交互必须的扩展。
ES包括：语法、类型、语句、关键字、保留字、操作符、全局对象。
大部分浏览器兼容ES6。
## 1.2.2 DOM
文档对象模型：是一个应用编程接口（API），用于在HTML中使用扩展的XML。DOM将整个页面抽象为一组分层节点。F12中常见的文档树。
![文档树](文档树.png)
DOM通过创建表示文档的树，让开发者可以更好地控制网页的内容和结构。使用DOM的API，可以轻松删除，添加，替换，修改节点。
DOM视图：描述追踪文档不同视图的接口。
DOM事件：描述事件及事件处理的接口。
DOM样式：描述处理元素CSS样式的接口。
DOM遍历的范围：描述遍历和操作DOM数的接口。
其他DOM：可伸缩矢量图（SVG），数学标记语言（MathML），同步多媒体集成语言（SMIL）
DOM有不同level（版本）:目前到了level3
## 1.2.3 BOM
浏览器对象模型：用于支持访问和操作浏览器的窗口。使用BOM，可以操控浏览器显示页面之外的部分，BOM针对浏览器窗口和子窗口。拓展：
弹出新浏览器窗口的能力；
移动、缩放和关闭浏览器窗口的能力；
navigator对象，提供关于浏览器的详尽信息；
location对象，提供浏览器加载页面的详尽信息；
screen对象，提供关于用户屏幕分辨率的详尽信息；
performance对象，提供浏览器内存占用、导航行为和时间统计的详尽信息；
对cookie的支持；
其他自定义对象，XMLHttp，ActiveXObject；
# 1.3 JavaScript版本
# 1.4 小结
JS是一门用来与网页交互的脚本语言，包含以下三个组成部分。
ES：有ECMA-262定义并提供核心功能。
文档对象模型（DOM）:提供与网页内容交互的方法和接口。
浏览器对象模型（BOM）：提供与浏览器交互的方法和接口。
JS这三个部门得到了五大Web浏览器不同程度的支持。所有浏览器基本上对ES5提供了完善的支持，ES6最佳。
---
# 2.1 <script>元素
将Js插入HTML的主要方法是使用<script>元素。有下列8个属性：
1.async：可选，表示立即开始下载脚本，但不能阻止其他页面动作，比如下载资源或等待其他脚本加载，只对外部脚本文件有效。
2.charset：可选，使用src属性指定的代码字符集。很少用。
3.crossorigin：可选，配置相关请求的CORS（跨源资源共享）设置。默认不使用CORS。
defer：可选，表示脚本可以延迟到文档完全被解析和显示之后再执行，只对外部脚本文件有效。
integrity：可选，允许比对接收到的资源和指定的加密签名以验证子资源完整性。
language：废弃。
src：可选，表示包含要执行的代码的外部文件。（引入外部JS文件）
type：可选，代替language，表示代码块中脚本语言的内容类型（MIME类型）。按照惯例这个值始终都是“text/JavaScript”，MIME类型通常都是“application/x-javascript”，如果这个值是module，则代码会被当成ES6模块，而且只有这时候代码中才能出现import和export关键字。
## 2.1.1 标签位置
<head>
<script src='example1.js'></script>
</head>
上述是把文件放在head里，不过这种写法以为着必须把所有JS代码都下载、解析和解释完成后，才能开始渲染页面，可能会导致页面渲染的明显延迟，所以通常把文件引用放在body元素中的页面内容后面。
<body>
<script src='example2.js'></script>
</body>
## 2.1.2 推迟执行脚本
可用defer属性，可用推迟脚本执行。
<script defer src='example1.js'></script>
## 2.1.3 异步执行脚本
<script async src='example1.js'></script>
## 2.1.4 动态加载脚本
JS可用使用DOM API ，通过向DOM中动态添加Script元素同样可用加载指定的脚本，只要创建一个Script元素并将其添加到DOM即可。如下：
let script = document.createElement('script');
script.src = 'gibbersh.js'
document.head.appendChild(script);
这个请求是异步的，不是所有浏览器都支持async属性，因此，如果要统一动态脚本的加载行为，可以明确将其设置为同步加载。
添加：script.async = false;
以这种方式获取的资源对浏览器预加载器是不可见的。这会严重影响它们在资源获取队列中的优先级。这种可能会严重影响性能。要想让预加载器知道这些动态请求文件的存在，可以在文档头部显示声明它们：
<link rel="preload" href="gibberish.js">
## 2.1.5 XMHTL中的变化
XHTML：可扩展超文本标记语言，是将HTML作为XML的应用重新包装的结果。在XHTML中使用JS必须制定type属性且值为text/javascript。
XHTML比较少见。
## 2.1.6 废弃的语法
个别废弃的语法，可不看。
# 2.2 行内代码与外部文件
最佳实践是尽可能将JS代码放在外部文件中。推荐原因如下：
可维护性：JS代码分散到很多HTML页面，会导致维护困难。而用一个目录保存所有JavaScript文件，则更容易维护，这样开发者就可以独立于使用它们的HTML页面来编辑代码。
缓存：浏览器会根据特定的设置缓存所有外部链接的JS文件，这意味着若干两个页面都用到同一个文件，则该文件只需下载一次。这最终意味着页面加载更快。
适应未来：通过把JS放到外部文件中，就不比考虑用XHTML的或注释黑科技。包含外部JS文件的语法在HTML和XHTML是一样的。
在配置浏览器请求外部文件时，要重点考虑的一点是它们会占用多少带宽。在SPDY/HTTP2中，预请求的消耗已显著降低，以轻量、独立JS组件形式向客户端送达脚本更具优势。
在初次请求时，如果浏览器支持SPDY/HTTP2，就可以从同一个地方取得一批文件，并将他们逐个放到浏览器缓存中。从浏览器角度看，通过SPDY/HTTP2获取所有这些独立的资源与获取一个大JS文件的 延迟差不多。
在第二个页面请求时，由于你已经把应用程序切割成了轻量可缓存的文件，第二个页面也依赖的某些组件此时已经存在于浏览器缓存中了。
# 2.3 文档模式
最初有两种模式：混杂模式，标准模式。
第三种模式：准标准模式。
# 2.4 <noscript>元素
针对不支持JS的浏览器而出的元素。以下两种情况，浏览器将显示包含在<noscript>中的内容：
浏览器不支持脚本；
浏览器对脚本的支持被关闭；
 <noscript> 
 <p>This page requires a JavaScript-enabled browser.</p> 
 </noscript>
# 2.5 小结
JS通过<script>元素插入到HTML页面中。这个元素可以用于把JS代码嵌入到HTML页面汇总，跟其他标记混合在一起，也可以用与引入保存在外部文件中的JS。本章的重点如下：
1.要包含外部JS文件，必须将src属性设置为要包含文件的URL。文件可以跟网页在同一台服务器上，也可以位于完全不同的域。
2.所有<script>元素会依照它们在网页中出现的次序被解释。在不使用defer和async属性的情况下，包含在<script>元素中的代码必须严格按次序解释。
3.对不推迟执行的脚本，浏览器必须解释完位于<script>元素中的代码，然后才能继续渲染页面的剩余部分。为此，通常把script元素放到页面末尾，介于主内容之后及</body>标签之前。
4.可以使用defer推迟到文档渲染完毕后再执行。推迟的脚本原则上按照它们被列出的次序执行。
5.可以使用async属性表示脚本不需要等待其他脚本，同时也不阻塞文档渲染，即异步加载。异步脚本不能保证按照它们在页面中出现的次序执行。
6.通过使用<noscript>元素，可以指定在浏览器不支持脚本时显示的内容。如果浏览器支持并启用脚本，则<noscript>元素中的任何内容都不会被渲染。
# 3.1 语法
## 3.1.1 区别大小写
ECMA中一切都区分大小写。无论是变量、函数名还是操作符，都区分大小写。
typeof不能作为函数名，因为它是一个关键字。但Typeof可以用。
## 3.1.2 标识符
变量、函数、属性或函数参数的名称。可以由一个或多个下列字符组成：
第一个字符必须是一个字母、下划线（_）或美元符号（$）;
剩下的其他字符可以是字母、下划线、美元符号或数字。
一般使用驼峰大小写形式。
## 3.1.3 注释
## 3.1.4 严格模式
"use strict" //脚本开头加上这一行
也可以在指定函数内加上开头。所有现代浏览器都支持严格模式。
## 3.1.5 语句
结尾建议加分号，建议语句块加{}
## 3.2 关键字与保留字
ES6的关键字有：
break 	do 	in 	typeof 
case 	else 	instanceof 	var 
catch 	export 	new 	void 
class 	extends 	return 	while 
const 	finally 	super 	with 
continue   for 	switch 	yield 
debugger function    this 
default 	if 	throw 
delete 	import 	try
ES6将来保留词汇：
始终保留：
enum
严格模式下保留：
implements 	package 	public 
interface	 protected 	static 
let 	private
模块代码中保留：
await
这些词汇不能作标识符，但可以坐对象的属性名，推荐不用作属性名。
# 3.3 变量
ECMA变量是松散类型的，变量可以用于保存任何类型的数据。每个变量不过是一个用于保存任意值的命名占位符。有3个关键字可以声明变量：var,const,let
var:声明完后可以赋值，但未标识类型。//声明提升
//var message = "hi"; 
//message = 100; // 合法，但不推荐。
//作用域在声明的环境下的函数作用域，例在函数内定义，调用完函数随即被销毁。
//在函数内定义时省略var操作符，可以创建一个全局变量。不推荐这么做。
let:块作用域，同一个块内不能重复声明。变量在作用域中无声明提升。
//有暂时性死区。
//无法全局声明，声明的变量不会成为window对象的属性。
//ES6不能依赖条件声明模式
const:与let基本相同，区别是声明变量时必须同时初始化变量，且无法修改const声明的变量。
## 3.3.4 声明风格及最佳实践
1.不使用var
2.const优先，let次之
# 3.4 数据类型
ES6有6种简单的数据类型（原始类型）：undefined,null,boolean,number,String,Symbol。Symbol是ES6新增的。还有一种复杂的数据类型叫Object（对象）。Object是一种无序名值对的集合。
## 3.4.1 typeof操作符
不需要参数（但可以使用参数），严格来说，函数也是对象，并不代表一种数据类型。可是函数也有自己特殊的属性。可以用typeof区分。
## 3.4.2 Undefined类型
变量未初始化即是Undefined，相当于给变量赋值了Undefined。
建议在声明时初始化，出现undefined可以更好辨别。
## 3.4.4 Null类型
Null类型同样只有一个值，即特殊值null。null值表示一个空对象指针，typeof null返回Object。
在定义将来要保存对象值的变量时，建议初始化为null。
## 3.4.4 Boolean类型
有两个字面值：true，false。
True和False是有效的标识符，不是布尔值。//区分大小写
使用Boolean()来转换类型
## 3.4.5 Number类型
1.浮点值
//小数点后面必须带数字，不然当整数处理。
2.值的范围
//Number.MIN_VALUE:5e-324
Number.MAX_VALUE:1.7976931348623157e+308
超出以上范围会表示为Infinity或-Infinity,该值无法用于计算。
可使用isFinite()函数进行判断
3.NaN
NaN表示"不是数值",用于表示本来要返回数值的操作失败了（不是抛出错误）。
例：0除任意数值
console.log(0/0) // NaN
console.log(5/0) //Infinity
console.log(5/-0)//-Infinity
任何涉及NaN的操作始终返回NaN，NaN不等于任何值。//(NaN == NaN)-->false
可用isNaN()函数判断是否不是数值
isNaN(NaN)//true
isNaN(10)//false
isNaN("10")//false,可转换为数值10
isNaN("blue")//true,无法转换为数值
isNaN(true)//false,可以转换为1
4.数值转换
有3个函数可以将非数值转换为数值：
Number(),parseInt(),parseFloat()
Number()是转型函数，可用于任何数据类型。后两个主要用于将字符串转为数值。
Number()有如下规则：
(true)->1,(false)->0,(null)->0,(undefined)->NaN,数值直接返回
如果字符串包含数值字符，包括数值字符前面带加号、减号的情况，则转换为一个十进制数值。
如果字符串包含有效的浮点值格式如“1.1”，则会转换为相应的浮点值（同样，忽略前面的0）。
如果字符串包含有效的十六进制格式如"0xf"，则会转换为与该十六进制值对应的十进制整数值。
如果是空字符串（不包含字符），则返回0。
如果字符串包含上述情况之外的其他字符，则返回NaN。
通常使用parseInt（）
## 3.4.6 String类型
字符串使用：双引号，单引号，反引号都合法，引号类型前后必须一致。
1.字面量：
\n  换行
\t   制表
\b  退格
\r   回车
\f   换页等
2.特点
不可变，一旦创建，值不能变。要修改某个变量的字符串值，必须先销毁原始的字符串，然后将包含新值的另一个字符串保存到该变量。
3.转换为字符串
toString()//函数
还可以传入参数输出不同进制
let num = 10;
num.toString() // "10"
num.toString(2) // "1010"
num.toString(8) // "12"
4.模板字面量
可以使用换行字符，可以跨行定义字符串。
使用反引号会保持引号内部的空格，字面量，length会增加。
5.字符串插值
可以在定义中插入一个或多个值。
通过反引号中使用 ${}插入，插入的值都会通过toString转换为字符串
插值表达式中可以调用函数和方法：
foo = {toString:() => 'Wrold'};`hello,${foo}` // hello world
capitalize(word) =>return `${word[0].toUpperCase()}`   // `${capitalize('hello')}`//->Hello
6.模板字面量标签函数
支持定义标签函数，通过标签函数可以自定义插值行为。
7.原始字符串
Unicode字符
使用String.raw获取原始字符串
'\u00A9' // 版权符号
String.raw`\u00A9`// \u00A9
## 3.4.7 Symbol类型
Symbol是ES6新增的，且实例是唯一，不可变的。用于创建唯一记号，进而用作非字符串形式的对象属性。
1.基本用法
let sym = Symbol(); type of sym//symbol
也可以传入字符串参数作为对symbol的描述，可通过这个字符串来调试代码。但这个字符串参数与符号定义或标识无关。
符号无法与new关键字一起作为构造函数使用。
可以使用符号包装对象，借用Object函数()函数：
let mySymbol = Symbol();
let myWrappedSymbol = Object (mySymbol);
console.log(typeof myWrappedSymbol); // "object"
2.使用全局符号注册表
如果运行时的不同部分需要共享和 重用符号实例，那么可以用一个字符串作为键，在全局符号注册表中创建并重用符号。
需要使用Symbol.for()方法。
## 3.4.8 Object类型
对象其实就是一组数据和功能的集合。可以通过new来创建实例对象。
每个对象都有如下属性和方法：
constructor：用于创建当前对象的函数，构造函数。
hasOwnProperty(propertyName)：用于判断当前对象实例上是否存在给定的属性。
isPrototypeOf(object)：用于判断当前对象是否为另一个对象的原型。
propertyIsEnumerable(propertyName):用于判断给定的属性是否可以使用。
toLacaleString():返回对象的字符串表示,反映对象所在本地化执行环境。
toString():返回对象的字符串表示。
valueOf():返回对象对应的字符串、数值或布尔值表示。
# 3.5 操作符
## 3.5.1 一元操作符
只操作一个值的操作符叫一元操作符。
++,--;  //操作中会自行转换类型,(递增和递减)
+,-//一元加减符，可以用于运算和转换
## 3.5.2 位操作符
~~~
## 3.5.3 布尔操作符
逻辑非，逻辑与逻辑或
1.逻辑非 ：！（感叹号）
!false // true
!"blue" //false
!0 //true
!NaN //true
!"" //true
!12345 //false
也可以用两个感叹号:!!,相当于调用了转型函数Boolean()。第一个返回布尔值，第二个对该布尔值取反。
相当于如上例子，布尔值取反。
2.逻辑与
由&&表示 // true && true为true  其余都为false
3.逻辑或
由||表示 //有一个是true为true，false || false为false
## 3.5.4 乘性操作符
乘法(*)，除法(/)，取模(%)。
乘法(*):都为数值则计算，有一项为NaN则返回NaN，如果是Infinity*0=NaN,Infinity*(-/+)num=(-)Infinity，Infinity*Infinity=Infinity,如果不是数值会转换后再近些操作。
除法(/):
0 / 0 = NaN,Infinity / Infinity = NaN,-(number)/0 = (-)Infinity,Infinity / (-)Number = (-)Infinity
取模(%):类似除
## 3.5.5 指数操作符
ES7新增的操作符 (**)//Math.pow(3,2) == 3 ** 2 == 9
squared ** = 2 //9
## 3.5.6 加性操作符
（+），（-）
## 3.5.7 关系操作符
（<）,（>）,（<=），（>=）
## 3.5.8 相等操作符
（==），（!=），（===）,（!==）
## 3.5.9 条件操作符
（?）// let max = （num1 > num2）? num1 : num2
## 3.5.10 赋值操作符
（=），（*=），（/=），（%=），（+=）,（-=）,（<<=）,（>>=）,（>>>=）
# 3.6 语句
## 3.6.1 if语句
~~~
## 3.6.2 do-while语句
do {***} while(expression);
## 3.6.3 while语句
let i = 0;
while(i < 10) { i += 2};
## 3.6.4 for语句
for(initialization;expression;post-loop-expression) statement
## 3.6.5 for-in语句
for(property in expression) statement
for(const propName in window) {document.write(propName)}//例子
## 3.6.6 for-of语句
for(property of expression) statement
for(const el of [2,4,6,8]){document.write(el)}//例子
## 3.6.7 标签语句
label:statement
start: for(let i = 0;i < count;i++){console.log(i)}//start是一个标签，可在后面通过break，continue语句引用。
## 3.6.8 break和continue语句
break用于立即退出循环,强行执行循环后的下一条语句。
continue语句用于立即退出循环，但会从循环顶部开始执行。
## 3.6.9 with语句
with(expression) statement;
let qs = location.search.substring(1);
let hostName = location.hostname;
let url = location.href;
with(location){
let qs = search.substring(1);
let hostName = hostname;
let url = href;
}
严格模式不允许使用
## 3.6.10 switch语句
switch(expression){
  case value1:
    statament
    break;
  case value2:
    statement
    break;
  ...
  default:
    statement
}
//switch不会强制转换数据类型
## 3.7 函数
function Name(arg0,arg1){ statements}
遇到return语句函数就会立即停止执行并退出。
函数不能以eval，arguments作为名称；
函数的参数不能叫eval，arguments；
两个命名参数不能拥有同一个名称。
## 3.8 小结
ES中基本数据类型包括：undefined,Null,Boolean,Number,String,Symbol
不需要指定函数的返回值，因为任何函数可以在任何时候返回任何值。//声明方式
不指定返回值的函数实际上会返回特殊值undefined。
# 4 变量、作用域与内存
## 4.1 原始值与引用值
变量有两种不同的类型：原始值和引用值。原始值就是最简单的数据，引用值则是由多个值构成的对象。
原始值的变量是按值访问的，引用值是保存在内存中的对象，操作对象时，操作的是对该对象的引用而非实际的对象本身。
### 4.1.1 动态属性
引用值可以随时添加、修改和删除其属性和方法。
只有引用值可以动态添加后面可以使用的属性。
原始类型的初始化可以只使用原始字面量形式。如果使用new则创建Object类型的实例。
let name1 = "wxc";//typeof name1 == string
let name2 = new String("Matt");//typeof name2 == object
### 4.1.2 复制值
原始值的变量复制会创建新变量。//let name1 = "wxc";let name2 = name1;
引用值的变量复制的是一个指针，两个变量指向同一个对象，一改则都改。
### 4.1.3 传递参数
函数的参数都是按值传递的，传递时，值会被复制到一个局部变量。
按引用传递参数时，值在内存中的位置会被保存在一个局部变量，对本地变量的修改会反映到函数外部。ES中函数的参数就是局部变量。
### 4.1.4确定类型
typeof对于原始值有用，但对引用值不大。
引用值判断可以用instanceof
person instanceof Object
colors instanceof Array
pattern instanceof RegExp
instanceof对于原始值始终返回false，原始值不是对象。
## 4.2 执行上下文与作用域
每个上下文都有一个关联的变量对象，这个上下文中定义的所有变量和函数都存在于这个对象上。
浏览器中，全局上下文为window对象。var定义的全局变量和函数都会成为window对象的属性和方法。使用let和const的顶级声明不会定义在全局上下文中，但在作用域链解析上效果是一样的。
每个函数也有自己的上下文，执行函数时，函数上下文被推倒一个上下文栈上，执行完后弹出。ES的执行流通过该上下文栈进行控制。
上下文中的代码在执行时，会创建变量对象的一个作用域链。这个作用域链决定了各级上下文中的代码在访问变量和函数时的顺序。正在执行的上下文的变量对象始终位于作用域链的最前端，如果上下文是函数，其活动对象用作变量对象。活动对象最初只有一个定义变量：arguments。作用域链的下一个变量对象来自上级包含上下文。全局上下文的变量对象始终是作用域链的最后一个变量对象。
局部作用域中定义的变量可用于在局部上下文中替换全局变量。
### 4.2.1 作用域链增强
代码执行到try/catch语句的catch块与with语句时，都会在作用域链前端添加一个变量对象。对with语句来说，会向作用域链前端添加指定的对象；对catch则会创建一个新的变量对象，这个变量对象会包含要抛出的错误对象的声明。
### 4.2.2 变量声明
1.使用var声明变量，变量会被自动添加到最接近的上下文，最接近的上下文大多是函数的局部上下文，如果未声明就被初始化了，就被添加到全局上下文。如果在函数内声明变量添加到全局上下文，函数退出后依然可以访问。
var声明会被拿到函数或全局作用域的顶部，位于作用域中所有代码之前。变量提升。
2.使用let声明的块级作用域声明
块级作用域由最近的{}界定。
3.使用const的常量声明
const声明的同时必须初始化为某个值。声明后不能重新赋新值。
作用域与let声明一样。
建议多使用const，除非需要一个会重新赋值的变量。可以防止重新赋值的BUG。
4.标识符查找
特定上下文读取或写入而引用一个标识符时，必须通过搜索确定这个标识符表示什么。搜索开始于作用域链前端，以给定的名称搜索对应的标识符。//其实就是调用变量
## 4.3 垃圾回收
JS使用垃圾回收，程序每隔一段就会自动运行。确定不会再使用的变量，释放内存。
### 4.3.1 标记清理
常用策略是标记清理。程序运行时，标记内存中存储的所有变量，将所有上下文中的变量，以及被在上下文中的变量引用的标记去掉。再加上标记代表待删除，随后做一次内存清理，销毁带标记的所有值并回收内存。
IE，Firefox，Opera，Chrome，Safari都在JS实习标记清理，频率有所差异。
### 4.3.2 引用计数
对每个值记录引用次数。声明变量并赋一个引用值时，这个值的引用数为1。 如果保存对该值引用的变量被其他值给覆盖了，引用数-1。引用数为0时回收内存。
### 4.3.3 性能
垃圾回收的时间调度很重要，变量太多会造成性能损失。JS引擎的垃圾回收程序被调优为动态改变分配变量、字面量或数组槽位等会触发垃圾回收的阈值。如果回收的内存不到已分配的15%，这些阈值会翻倍。如果一次回收的内存达到已分配的85%，则阈值重置为默认值。
### 4.3.4 内存管理
保证在执行代码时只保存必要的数据。不在必要则设置为null，从而释放其引用。这也可以叫作解除引用。局部变量在超出作用域会自动解除引用，所以该建议更适合全局变量和全局对象。
1.通过const和let声明提升性能
块作用域，能更早让垃圾回收程序介入。
2.隐藏类和删除操作
对象与隐藏类会被关联起来，用于跟踪他们的属性特征。共享相同隐藏类的对象性能会更好。
function Article(){this.title = 'go go go'}
let a1 = new Article();//隐藏类title
let a2 = new Article();//隐藏类title
a1.author = 'Jake'//对应多出author隐藏类，可能对性能产生明显影响。
function Article(author){this.title='go',this.author=author}
let a2 = new Article('wxc')//a2与a1相同，共享一个隐藏类。
delete a1.author//使用delete关键字会导致生成同样的隐藏类片段
a1.author = null; //保持共享，并达到垃圾回收的效果
3.内存泄漏
JS的内存泄漏大部分是不合理的引用导致的。
function(){name = 'Jake'}意外声明全局变量是最常见也最容易修复的内存泄漏问题。无关键字声明。
定时器也会导致内存泄漏，定时器的回调通过闭包引用了外部变量。
使用闭包容易造成内存泄漏，如下：
let outer = function() {let name = 'Jake';return function() {return name};};
调用outer()会导致内存泄漏。只要返回的函数存在就不能清理name，因为闭包一直在引用，加入name的内容很大，就是个大问题。
4.静态分配与对象池
不要动态创建矢量对象
在初始化的时候，创建一个对象池，管理一组可回收的对象。使用完后回归对象池。
## 4.4 小结
原始值大小固定，因此保存在栈内存上。
引用值是对象，存储在堆内存上。
任何变量都存在于某个作用域（上下文）中，这个作用域决定了变量的声明周期，以及它们可以访问代码的哪些部分。
全局上下文：window，浏览器。
函数上下文：声明函数的{}内
块级上下文：最近的{}内
JS有垃圾回收，垃圾回收的方法有：引用计数，标记清理。主流为标记清理。
接触变量引用一般直接给变量赋值为null。
# 5.基本引用类型
引用值是某个特定引用类型的实例。
对象被认为是某个特定引用类型的实例。新对象通过使用new操作符跟一个构造函数来创建。
函数也是一种引用类型。
## 5.1 Date
日期对象//let now = new Date();
可用Date.parse()转换成日期对象//let someDate = new Date(Date.parse("May 23,2019"));如果字符串不表示日期，会返回NaN。
let allFives = new Date(Date.UTC(2005,4,5,17,55,55));//GMT时间——Date.UTC方法
ES提供了Date.now()方法，返回表示方法执行时日期。
let start = Date.now();//当前时间
### 5.1.1 继承的方法
let date = new Date(2021,1,20);
toLocaleString()//-->2021/2/20 上午12:00:00
toString()//-->Sat Feb 20 2021 00:00:00 GMT+0800
valueOf()//-->1613750400000
### 5.1.2 日期格式化方法
Date格式化日期的方法：
toDateString()//显示日期中的周几，月，日，年
toTimeString()//显示日期中的时分秒和时区
toLocaleDateString()//显示日期中的周几 月 日 年
toLocaleTimeString()//显示日期中的时 分 秒
toUTCString()//显示完整的UTC日期
### 5.1.3 日期/时间组件方法
主要应用：
getTime()//返回日期的毫秒表示，与valueOf相同
setTime(milliseconds)//设置日期的毫秒表示，从而修改整个日期
getFullYear()//返回四位年数
getMonth()//返回日期的月
getDate()//返回日期的日
getDay()//返回日期中表示周几的数值
getHours()//返回日期中的时
getMinutes()//返回日期中的分
getSeconds()//返回日期中的秒
## 5.2 RegExp
ES通过RegExp类型支持正则表达式。
let expression = /pattern/flags;
匹配模式的标记：
1.g:全局模式，表示查找字符串的全部内容，而不是找到第一个匹配的内容就结束。
2.i:不区分大小写，表示查找匹配时忽略pattern和字符串的大小写。
3.m:多行模式，表示查找到一行文本末尾时会继续查找。
4.y:粘附模式，表示只查找从lastIndex开始及之后的字符串。
5.u:Unicode模式，启用Unicode匹配。
6.s：dotAll模式，表示元字符匹配任何字符。(包括\n或\r)。
使用不同模式和标记可以创建出各种正则表达式，比如：
//匹配字符串中的所有"at"
let pattern1 = /at/g;
//匹配第一个"bat"或"cat" 忽略大小写
let pattern2 = /[bc]at/i
//匹配所有以"at"结尾的三字符组合，忽略大小写
let pattern3 = /.at/gi
元字符在模式中必须转义：
( ，[， {，\，^，$，|，)，]，}，？，*，+，- //这些符号前面需要\来转义
//匹配第一个"bat"或"cat"，忽略大小写
let pattern1 = /[bc]at/i;
//匹配第一个"[bc]at"，忽略大小写
let pattern2 = /\[bc\]at/i;
//匹配所有以"at"结尾的三字符组合，忽略大小写
let pattern3 = /.at/gi;
//匹配所有".at"，忽略大小写
let pattern4 = /\.at/gi;
也可使用RegExp构造函数来创建：
let pattern1 = /[bc]at/i   ==   new RegExp("[bc]at","i");
也可以使用实例，选择性修改标记
const re1 = /cat/g;
const re2 = new RegExp(re1);
const re3 = new RegExp(re1,"i");
### 5.2.1 RegExp实例属性
global:布尔值，表示是否设置了g标记。
ignoreCase:布尔值，表示是否设置了i标记。
unicode:布尔值，表示是否设置了u标记。
sticky:布尔值，表示是否设置了y标记。
lastIndex:整数，表示在源字符串中下一次搜索的开始位置，始终从0开始。
multiline:布尔值，表示是否设置了m标记。
dotAll:布尔值，表示是否设置了s标记。
source:正则表达式的字面量字符串，没有开头和结尾的斜杠。
flags:正则表达式的标记字符串。始终以字面量而非传入构造函数的字符串模式形式返回。
### 5.2.2 RegExp实例方法
exec()函数：
let text = 'cat, bat, sat, fat';
  let pattern = /.at/gi;
  let matchs = pattern.exec(text);
  console.log(matchs);//cat
//设置了全局标记(g)，每次调用返回一个匹配的信息，如果没有设置全局标记，只会返回第一个匹配的信息。
//设置了g标记，每次调用exec()都会在字符中向前搜索下一个匹配项
let text = 'cat, bat, sat, fat';
  let pattern = /.at/gi;
  let matchs = pattern.exec(text);//cat
  let matchs = pattern.exec(text);//bat
  let matchs = pattern.exec(text);//sat
  console.log(matchs);
//设置了y标记，每次调用会在lastIndex的位置上寻找匹配项。y标记覆盖g标记。
test()函数：//用于判断是否存在实际内容中，常在if判断语句中
let text = "000-00-00 00";
let pattern = /\d{3}-\d{2}-\d(4)/;
if(pattern.test(text)) {console.log("The pattern was matched.")};
继承的方法toLocaleString()和toString()都返回字面量表示。
let pattern = new RegExp("\\[bc\\]at","gt");
console.log(pattern.toString());//  /\[bc\]at/gi
console.log(pattern.toLocaleString());//  /\[bc\]at/gi
### 5.2.3 RegExp构造函数属性
input：$_   //最后搜索的字符串
lastMatch：$&   //最后匹配的文本
lastParen：$+   //最后匹配的捕获组
leftContext：$`   //input字符串中出现在lastMatch前面的文本
rightContext：$'   //input字符串中出现在lastMatch后面的文本
let text = "this has been a short summer";
let pattern = /(.)hort/g; //()-->捕获组
if(pattern.test(text)) {
   console.log(RegExp.input); //this has been a short summer
   console.log(RegExp.leftContext); //this has been a
   console.log(RegExp.rightContext); //summer
   console.log(RegExp.lastMatch); //short
   console.log(RegExp.input); //s
}

if(pattern.test(text)) {
   console.log(RegExp.$_); //this has been a short summer
   console.log(RegExp["$`"]); //this has been a
   console.log(RegExp["$'"]); //summer
   console.log(RegExp["$&"]); //short
   console.log(RegExp["$+"]); //s
}
let pattern = /(..)or(.)/g;

if(pattern.test(text)) {
   console.log(RegExp.$1); // sh
   console.log(RegExp.$2);// t
}
### 5.2.4 模式局限
ES对正则表达式的支持还缺少一些高级特性。
## 5.3 原始值包装类型
ES提供了3种特殊类型的引用类型：Boolean,Number,String。
以读模式访问字符串时，后台执行：
（1）创建一个String类型的实例；// let s1 = "some text"
（2）调用实例上的特点方法；// let s2 = s1.substring(2);
（3）销毁实例；// s1 = null;
let value = "25";
let number = Number(value);   //转型函数
console.log(typeof number);   //"number"
let obj = new Number(value); // 构造函数
console.log(typeof obj); //"object"
变量obj保存一个Number实例。
### 5.3.1 Boolean
let falseObject = new Boolean(false);// typeof == object
let result = falseObject && true;
console.log(result); //true  
let falseValue = false;//typeof == boolean 强烈建议永远不要使用
result = falseValue && true;
console.log(result); //false
### 5.3.2 Number
方法：toFix()//let num = 10;num.toFixed(2);// "10.00"
方法：toExponential()//let num = 10;num.toExponential(1);//"1.0e+1"
方法：toPrecision()//let num = 99;
num.toPrecision(1)//"1e+2"
num.toPrecision(2)//"99"
num.toPrecision(3)//"99.0"
方法：isInterger()//辨别一个数值是否保存为整数。
Number.isInterger(1);// true
Number.isInterger(1.00)//true
Number.isInterger(1.01)//false
方法：isSafeInterger()判断数值范围
### 5.3.3 String
每个字符用16位表示，基于16位码元完成操作。//基本多语言平面。
normalize()方法：用于判断规范性。
concat()：拼接//用加法运算符也可
Value = "hello world";
slice()：
Value.slice(3)//"lo world";
Value.slice(3,7)//"lo w";
Value.slice(-3)//"rld" 等同于slice(8);(11-3)
Value.slice(3,-4)//"lo w" 等同于slice(3,7);(3+4)
substr()：
Value.substr(3)//"lo world";
Value.substr(3,7)//"lo worl";
Value.substr(-3)//"rld" 等同于substr(8);
Value.substr(3,-4)//""等同于substr(3,0);
substring()：
Value.substring(3)//"lo world";
Value.substring(3,7)//"lo w";
Value.substring(-3)//"hello world" 等同于substring(0)
Value.substring(3,-4)//"hel"等同于substring(0,3)
indexOf():
Value.indexOf("o");// 4
Value.indexOf("t")// -1
Value.indexOf("o",6)//7
lastIndexOf():
Value.lastIndexOf("o")//7
Value.lastIndexOf("t")//-1
Value.lastIndexOf("o",6)//4
message = "foobarbaz";
startWith():
message.startWith("foo");//true
message.startWith("bar");//false
endWith():
message.endWith("baz");//true
message.endWith("bar");//false
includes():
message.includes("bar");//true
message.includes("qux");//false
trim()://不影响原字符串，trimLeft(),trimRight()
let string = "   hello  world   ";
string.trim()//"hello  world"
repeat():
string = "abc";
string.repeat(2)//"abcabc";
padStart(),padEnd():
string = "foo"
string.padStart(6)//"   foo";len=6
string.padStart(9,".")//"......foo";len=9
string.padStart(8,"bar")//"barbafoo"len=8
string.padEnd(6)//"foo   ";
string.padEnd(9,".")//"foo......";
string.padEnd(8,"bar")//"foobarba";
迭代与解构
let message = "abc";
Iterator = message[Symbol.iterator]();
Iterator.next()//{value:"a",done:false}
Iterator.next()//{value:"b",done:false}
Iterator.next()//{value:"c",done:false}
Iterator.next()//{value:"undefined",done:true}
大小写转换
toLowerCase()//小写
toLocalLowerCase()//特定地区方法使用
toUpperCase()//大写
toLocalUpperCase()//特定地区方法使用
字符串模式匹配方法
match():与exec()方法一致
search():
let text = "cat, bat, sat, fat";
let pos = text.search(/at/);//1第一个位置为1
replace():
let res = text.replace("at","ond");//"cond, bat, sat, fat"
let res = text.replace(/at/g,"ond")//"cond, bond, sond, fond"
localeCompare():按字母表顺序比较返回值
## 5.4 单例内置对象
包括Global,Math
### 5.4.1 Global
全局作用域中定义的变量和函数都会成为Global对象的属性。
encodeURI(),encodeURIComponent()//编码统一资源标识符。
eval():
eval("console.log('hi')");///console.log("hi");
eval("function sayHi(){console.log('hi');}");///sayHi();
容易被XSS攻击。
对象属性：
undefined//特殊值
NaN//特殊值
Infinity//特殊值
Object//构造函数
Array//构造函数
Function//构造函数
....
window对象
window为Global对象的代理,全局变量和函数即为window的属性。
### 5.4.2 Math
Math对象属性：
E //自然对数的基数e的值
LN10 //10为底的自然对数
LN2 //2为底的自然对数
LOG2E //以2为底e的对数
LOG10E //以10为底e的对数
PI //π的值
SQRT1_2 //1/2的平方根
SQRT2 //2的平方根
Math方法：
min():取最小值//配合数组可以使用扩展操作符
max():取最大值//max = Math.max(...array);
ceil():向上取
Math.ceil(25.9);//26
Math.ceil(25.5);//26
Math.ceil(25.1);//26
round():四舍五入
console.log(Math.round(25.9)); // 26 
console.log(Math.round(25.5)); // 26 
console.log(Math.round(25.1)); // 25
fround():取单精度浮点值
console.log(Math.fround(0.4)); // 0.4000000059604645 
console.log(Math.fround(0.5)); // 0.5 
console.log(Math.fround(25.9)); // 25.899999618530273
floor():向下取
console.log(Math.floor(25.9)); // 25 
console.log(Math.floor(25.5)); // 25 
console.log(Math.floor(25.1)); // 25
random()://返回小数0~1内
加密提高不确定性：建议使用window.crypto.getRandomValues()。
abs()//绝对值
exp()//次幂
log()//自然对数
....
## 5.5 小结
对象为引用值，内置的引用类型可用于创建特定类型的对象。
RegExp是ES支持正则表达式的接口。
函数实际上是Function类型的实例，是对象。
# 6 集合引用类型
## 6.1 Object
let person = new Object();//构造函数
person.name = 'micheal';
let person = {name:'micheal'};//{}字面量表达式
person["name"]//micheal
person.name//micheal
## 6.2 Array
### 6.2.1 创建数组
let colors = new Array();//可以传值创建初始length的数组，也可以传数组值
let colors = ["red","blue"]//字面量表达式
from():
Array.from("Matt")//["M","a","t","t"]
适用于Map,Set,Array,iterator,arguments
of()://使用Array.prototype.slice.call(arguments)
Array.of(1,2,3,4)//[1,2,3,4]
Array.of(undefined)//[undefined]
### 6.2.2 数组空位
使用(,)创建数组空位
const options = [,,,,,]
options.length = 5
options //[,,,,,]
空值为undefined
options = [1,,,5];
options.map(()=>6)//[6,,,6]
options.join('-')//"1-----5"
### 6.2.3 数组索引
colors[0]-->第一个元素
给数组设置length会改变数组大小
### 6.2.4 检测数组
判断是否数组，使用instanceof
也可使用isArray()方法
### 6.2.5 迭代器方法
const a = ["a","b","c","d"];
keys()://返回数组索引的迭代器
const akeys = Array.from(a.keys()); // [0,1,2,3]
values()://返回数组元素的迭代器
const aValues = Array.from(a.Values());//["a","b","c","d"]
entries()://返回索引/值对的迭代器
const aEntries = Array.from(a.entries());//[[0,"a"],[1,"b"],[2,"c"],[3,"d"]]
for(const [idx,element] of a.entries()){
alert(idx);
alert(element);
}
//0
//a
//1
//b
//2
//c
//3
//d
### 6.2.6 复制和填充方法
copyWithin()//批量复制
fill()://填充
const a = [0,0,0,0,0];
zeros.fill(5)//[5,5,5,5,5];
zeros.fill(6,3)//[0,0,0,6,6]
zeros.fill(7,1,3)//[0,7,7,0,0]
索引过低，过高，反向都会被忽略
部门可用的索引，填充可用部分。
ints = [0,1,2,3,4,5,6,7,8,9];
ints.copyWithin(5) // [0,1,2,3,4,0,1,2,3,4];
ints.copyWithin(0,5)//[5,6,7,8,9,5,6,7,8,9];
ints.copyWithin(4,0,3)//[0,1,2,3,0,1,2,7,8,9];
ints.copyWithin(2,0,6)//[0,1,0,1,2,3,4,5,8,9];
### 6.2.7 转换方法
数组调用toString(),valueOf()方法相当于每个元素调用一次这个方法。
### 6.2.8 栈方法
push()//从最后推入数据
pop()//弹出最后一项并返回
### 6.2.9 队列方法
shift()://删除数组第一项并返回
push()://从最后推入数据
unshift()://从开头推入
### 6.2.10 排序方法
reverse()://反向排序
sort()://将元素转换成字符串比较
### 6.1.11 操作方法
concat():添加//直接使用会打平数组
slice():取值
splice()://可实现删除(两个参数)，插入(三个参数)，替换(三个参数)
### 6.2.12 搜索和位置方法
indexOf()//查找元素位置，返回
lastIndexOf()//查找元素位置，返回
includes()//返回布尔值，是否包含元素
find()//返回第一个匹配的元素
findIndex()//返回索引
### 6.2.13 迭代方法
every():元素都匹配才会返回true
filter():返回true的元素组成数组返回
forEach():运行函数，无返回值
map():调用结果构成数组返回
some():如果有一项返回true，则返回true
### 6.2.14 归并方法
reduce():从头遍历,构建一个返回值
reduceRight():从尾遍历,构建一个返回值
## 6.3 定型数组
### 6.3.1 历史
WebGL用到，3D技术。
定型数组
### 6.3.2 ArrayBuffer
构造函数，用于内存中分配特定数量的字节空间。
### 6.3.3 DataView
### 6.3.4 定型数组
## 6.4 Map
一种实现键值存储机制的集合类型。
### 6.4.1 基本API
const m2 = new Map([["key1","val1"]["key2","val2"]["key3","val3"]])
m1.size = 3
可使用has(),get()进行查询，delete(),clear()删除值。
### 6.4.2 顺序与迭代
提供迭代器(Iterator),通过entries()获取
可以通过遍历获取。
### 6.4.3 选择Object还是Map
1.内存占用
Map占用更小
2.插入性能
Map插入性能更好
3.查找速度
Object优于Map
4.删除性能
Map更快，涉及大量删除 Map最佳。
## 6.5 WeakMap
类似于Map，只能用对象作为键。
API与Map相同。
键不存在时，值会被垃圾回收。
无法迭代。
## 6.6 Set
### 6.6.1 基本API
与Map相似，size长度，has()查询，delete()和clear()删除元素。
add()添加元素。
### 6.6.2 顺序与迭代
可通过values()与keys()获取迭代器
可以使用遍历方法迭代。
## 6.7 WeakSet
与WeakMap类型
## 6.8 迭代与扩展操作
支持for-of循环
支持浅拷贝
let arr1 = [...arr2];
## 6.9 小结
JS的对象是引用值，可以通过几种内置引用类型创建特定类型的对象。
Object类型是一个基础类型，所有引用类型都继承了它的基本行为。
Array是一组有序的值，并提供了操作和转换值的能力。
定型数组包含一套不同的引用类型。
Date，日期类型。RegExp，正则表达式的接口。
ES6新增Map，WeakMap,Set,WeakSet。
# 7 迭代器与生成器
迭代即“重复”，“再来”。
## 7.1 理解迭代
JS中，计数循环就是一种最简单的迭代：for（）
可以指定顺序，次数，在一个有序集合上进行。
需知道如何使用数据结构，遍历顺序不是数据结构固有的。
## 7.2 迭代器模式
任何实现Iterable接口的数据结构都可以被实现Iterator接口的结构消费。
迭代器是按需创建的一次性对象。每个迭代器都会关联一个可迭代对象。
### 7.2.1 可迭代协议
实现了Iterable接口的内置类型：
1.字符串
2.数组
3.映射
4.集合
5.arguments对象
6.NodeList等DOM集合类型
接受可迭代对象的语言特性包括：
let arr = ["foo","bar","baz"];
1.for-of //for(let el of arr){el};
2.数组解构 //let [a,b,c] = arr;
3.扩展操作符 // let arr2 = [...arr];
4.Array.from() //let arr3 = Array.from(arr); 
5.创建集合 //let set = new Set(arr);
6.创建映射 //let pairs = arr.map((x,i)=>[x,i]);
7.promise.all()
8.promise.race()
9.yield*操作符
### 7.2.2 迭代器协议
let arr = ["a","b"];
console.log(arr[Symbol.iterator]); //f values(){[native code]};
let iter = arr[Symbol.iterator]();
console.log(iter);// ArrayIterator()
iter.next();//{done:false,value:"a"};
### 7.2.3 自定义迭代器
自定义迭代方法
### 7.2.4 提前终止迭代器
return {done:true};
或break
## 7.3 生成器
### 7.3.1 生成器基础
### 7.3.2 通过yield中断执行
### 7.3.3 生成器作为默认迭代器
### 7.3.4 提前终止生成器
## 7.4 小结
由任意对象实现的接口，支持连续获取对象产出的每一个值。使用symbol.iterator获取，并且通过一些方法调用，例next(),for-of。
# 8 对象、类与面向对象编程
无特定顺序的值。每个属性或方法都用名称标识。
## 8.1 理解对象
### 8.1.1 属性的类型
数据属性：
[[Configurable]]:表示属性是否可以通过delete删除并重定义，是否可修改特性，是否可以把它改为访问器属性。
[[Enumerable]]:表示属性是否可以通过for-in循环返回。
[[Writable]]:表示属性的值是否可以被修改。
[[Value]]:表示属性的值。
访问器属性：
[[Configurable]]:表示属性是否可以通过delete删除并重定义，是否可修改特性，是否可以把它改为访问器属性。
[[Enumerable]]:表示属性是否可以通过for-in循环返回。
[[Get]]:获取函数，读取属性调用。
[[Set]]:设置函数，写入属性时调用。
### 8.1.2 定义多个属性
let book = {};
Object.defineProperties(book,{year:{value:2017},edition:{value:1},year:{get(){return this.year;}}});
### 8.1.3 读取属性的特性
Object.getOwnPropertyDescriptor(object,'name');
descriptor = Object.getOwnPropertyDescriptor(book,"year");
Object.getOwnPropertyDescriptors(object);//获取所有
### 8.1.4 合并对象
Object.assgin();//浅拷贝,会覆盖重复的属性
result = Object.assign(object1,object2);
object === result
result = Object.assign(object1,object2,object3);
### 8.1.5 对象标识及相等判定
Object.is()//需要两个参数
Object.is(+0,-0)//false
### 8.1.6 增强的对象语法
let person = {name:name};  === let person = {name};//不建议
namekey = "name";let person = {[namekey]:'Matt'};//[]内可以使用表达式，属性可计算
let person = {[nameKey](name){console.log('name')}};//方法名兼容计算属性
### 8.1.7 对象解构
let person = {name:'matt',age:27}//不解构
let personName = person.name,personAge = person.age;//解构
let {name:personName,age:personAge} = person;
null和undefined不支持解构

let person = {job:{title:'Software engineer'}};//嵌套解构
let personCopy={};
let({job:personCopy.job}=person);

前面的解构出错，后面的解构会失败。

let person = {name:'matt',age:27}; function printPerson(foo,{name,age},bar)//参数解构，调用时传入对象
## 8.2 创建对象
### 8.2.1 概述
与类不同，对象的巧妙运行可以实现与类相同的行为。
### 8.2.2 工厂模式
设计模式之一
function createPerson(name,age,job){
   let o = new Object();
   o.name = name;
   o.age = age;
   o.job = job;
   o.sayName = function(){
       console.log(this.name);
   };
   return o;
}
解决创建多个类似对象的问题，但无解决对象标识问题（对象类型）。
### 8.2.3 构造函数模式
function Person(name,age,job){
   this.name = name;
   this.age = age;
   this.job = job;
   this.sayName = function(){
      console.log(this.name);
   }
}
与工厂模式类似,无return，无显式创建对象。
构造函数不一定写成函数声明的形式。赋值给变量的函数表达式也可。
let person = function(){};
let person1 = new person(...);
let person2 = new person(...);
person1 instanceof Object//true
person1 instanceof person//true
person2一样
构造函数也可以直接调用
person(...);window.sayName();//添加到了window
let o = new Object();
Person.call(o,"wxc",25);o.sayName()//wxc 在另一个对象的作用域中调用
在构造函数内定义的函数实例化后相同名称确不相等，是两个不同的函数。
可以在外部定义函数，在内部赋值解决这个问题。
### 8.2.4 原型模式
prototype,这个属性为一个对象。包含由特定引用类型的实例共享的属性和方法。实际上是构造函数创建的原型。
在原型上定义的值可以共享。
Chrome暴露了_proto_属性，可通过这个属性访问对象的原型。prototype属性为对象。
原型链会终止与Object的原型链。
person.prototype._proto_._proto_ === null//true
构造函数、原型对象和实例，三个完全不同的对象。
实例通过_proto_链接到原型对象，实际指向[[Prototype]]
构造函数通过prototype属性链接到原型对象。
同一个构造函数创建的两个实例，共享一个原型对象。
isPrototypeOf()//用于判断实例原型对象与构造函数的原型相同否
P227
