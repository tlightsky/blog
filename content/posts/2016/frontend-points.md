---
layout: post
title:  "前端知识点梳理"
date:   2016-03-09 11:23:57
categories: frontend points
---


## position的值， relative和absolute分别是相对于谁进行定位的？


- `absolute` :生成绝对定位的元素， 相对于最近一级的 定位不是 static 的父元素来进行定位。

- `fixed` （老IE不支持）生成绝对定位的元素，相对于浏览器窗口进行定位。

- `relative` 生成相对定位的元素，相对于其在普通流中的位置进行定位。

- `static`  默认值。没有定位，元素出现在正常的流中

<br>

## 谈谈你会webpack的看法



`WebPack` 是一个模块打包工具，你可以使用`WebPack`管理你的模块依赖，并编绎输出模块们所需的静态文件。它能够很好地管理、打包Web开发中所用到的`HTML、Javascript、CSS`以及各种静态文件（图片、字体等），让开发过程更加高效。对于不同类型的资源，`webpack`有对应的模块加载器。`webpack`模块打包器会分析模块间的依赖关系，最后 生成了优化且合并后的静态资源。


`webpack`是加强版的`Browserify`。



`webpack`的两大特色：



    1.code splitting（可以自动完成）

    2.loader 可以处理各种类型的静态文件，并且支持串联操作

### webpack的优势：



- `require.js`的所有功能它都有。

- 编绎过程更快，因为`require.js`会去处理不需要的文件


`webpack` 是以` commonJS `的形式来书写脚本滴，但对 `AMD/CMD` 的支持也很全面，方便旧项目进行代码迁移。



`webpack`具有`requireJs`和`browserify`的功能，但仍有很多自己的新特性：


```
1. 对 CommonJS 、 AMD 、ES6的语法做了兼容

2. 对js、css、图片等资源文件都支持打包

3. 串联式模块加载器以及插件机制，让其具有更好的灵活性和扩展性，例如提供对CoffeeScript、ES6的支持

4. 有独立的配置文件webpack.config.js

5. 可以将代码切割成不同的chunk，实现按需加载，降低了初始化时间

6. 支持 SourceUrls 和 SourceMaps，易于调试

7. 具有强大的Plugin接口，大多是内部插件，使用起来比较灵活

8.webpack 使用异步 IO 并具有多级缓存。这使得 webpack 很快且在增量编译上更加快
```

#### XSS原理及防范

Xss(cross-site scripting)攻击指的是攻击者往Web页面里插入恶意 `html`标签或者`javascript`代码。比如：攻击者在论坛中放一个

看似安全的链接，骗取用户点击后，窃取`cookie`中的用户私密信息；或者攻击者在论坛中加一个恶意表单，

当用户提交表单的时候，却把信息传送到攻击者的服务器中，而不是用户原本以为的信任站点。



#### XSS防范方法

首先代码里对用户输入的地方和变量都需要仔细检查长度和对`”<”,”>”,”;”,”’”`等字符做过滤；其次任何内容写到页面之前都必须加以`encode`，避免不小心把`html tag` 弄出来。这一个层面做好，至少可以堵住超过一半的`XSS` 攻击。


首先，避免直接在`cookie` 中泄露用户隐私，例如email、密码等等。



其次，通过使`cookie` 和系统`ip` 绑定来降低`cookie` 泄露后的危险。这样攻击者得到的`cookie` 没有实际价值，不可能拿来重放。



尽量采用`POST` 而非`GET` 提交表单


### HTTP和HTTPS



`HTTP`协议通常承载于TCP协议之上，有时也承载于`TLS`或`SSL`协议层之上，这个时候，就成了我们常说的HTTPS。



默认HTTP的端口号为80，`HTTPS`的端口号为443。



### 为什么`HTTPS`安全

因为网络请求需要中间有很多的服务器路由器的转发。中间的节点都可能篡改信息，而如果使用`HTTPS`，密钥在你和终点站才有。`https`之所以比`http`安全，是因为他利用`ssl/tls`协议传输。它包含证书，卸载，流量转发，负载均衡，页面适配，浏览器适配，refer传递等。保障了传输过程的安全性

### 什么是Etag？


当发送一个服务器请求时，浏览器首先会进行缓存过期判断。浏览器根据缓存过期时间判断缓存文件是否过期。<br>

情景一：若没有过期，则不向服务器发送请求，直接使用缓存中的结果，此时我们在浏览器控制台中可以看到  `200 OK`(from cache) ，此时的情况就是完全使用缓存，浏览器和服务器没有任何交互的。


情景二：若已过期，则向服务器发送请求，此时请求中会带上①中设置的文件修改时间，和`Etag`



然后，进行资源更新判断。服务器根据浏览器传过来的文件修改时间，判断自浏览器上一次请求之后，文件是不是没有被修改过；根据`Etag`，判断文件内容自上一次请求之后，有没有发生变化

情形一：若两种判断的结论都是文件没有被修改过，则服务器就不给浏览器发`index.html`的内容了，直接告诉它，文件没有被修改过，你用你那边的缓存吧—— `304 Not Modified`，此时浏览器就会从本地缓存中获取`index.html`的内容。此时的情况叫协议缓存，浏览器和服务器之间有一次请求交互。<br>

情形二：若修改时间和文件内容判断有任意一个没有通过，则服务器会受理此次请求，之后的操作同①

<br>

① 只有get请求会被缓存，post请求不会


### 栈和堆的区别？



    栈区（stack）—   由编译器自动分配释放   ，存放函数的参数值，局部变量的值等。

    堆区（heap）   —   一般由程序员分配释放，   若程序员不释放，程序结束时可能由OS回收。

    堆（数据结构）：堆可以被看成是一棵树，如：堆排序；

    栈（数据结构）：一种先进后出的数据结构。

### ES6的了解

新增模板字符串（为JavaScript提供了简单的字符串插值功能）、箭头函数（操作符左边为输入的参数，而右边则是进行的操作以及返回的值`Inputs=>outputs`。）、`for-of`（用来遍历数据—例如数组中的值。）`arguments`对象可被不定参数和默认参数完美代替。`ES6`将`promise`对象纳入规范，提供了原生的`Promise`对象。增加了`let`和`const`命令，用来声明变量。增加了块级作用域。let命令实际上就增加了块级作用域。ES6规定，`var`命令和`function`命令声明的全局变量，属于全局对象的属性；`let`命令、`const`命令、`class`命令声明的全局变量，不属于全局对象的属性。。还有就是引入`module`模块的概念



### js继承方式及其优缺点



>原型链继承的缺点


    一是字面量重写原型会中断关系，使用引用类型的原型，并且子类型还无法给超类型传递参数。


>借用构造函数（类式继承）



    借用构造函数虽然解决了刚才两种问题，但没有原型，则复用无从谈起。所以我们需要原型链+借用构造函数的模式，这种模式称为组合继承



>组合式继承



    组合式继承是比较常用的一种继承方法，其背后的思路是 使用原型链实现对原型属性和方法的继承，而通过借用构造函数来实现对实例属性的继承。这样，既通过在原型上定义方法实现了函数复用，又保证每个实例都有它自己的属性。

具体请看：[JavaScript继承方式详解](http://segmentfault.com/a/1190000002440502)



### 谈谈浮动和清除浮动

浮动的框可以向左或向右移动，直到他的外边缘碰到包含框或另一个浮动框的边框为止。由于浮动框不在文档的普通流中，所以文档的普通流的块框表现得就像浮动框不存在一样。浮动的块框会漂浮在文档普通流的块框上。



### 如何评价AngularJS和BackboneJS

`backbone`具有依赖性，依赖`underscore.js`。`Backbone + Underscore + jQuery(or Zepto)` 就比一个`AngularJS` 多出了2 次HTTP请求.

<br>

`Backbone`的`Model`没有与UI视图数据绑定，而是需要在View中自行操作DOM来更新或读取UI数据。`AngularJS`与此相反，Model直接与UI视图绑定，`Model`与UI视图的关系，通过`directive`封装，`AngularJS`内置的通用`directive`，就能实现大部分操作了，也就是说，基本不必关心`Model`与UI视图的关系，直接操作Model就行了，UI视图自动更新。

<br>

`AngularJS`的`directive`，你输入特定数据，他就能输出相应UI视图。是一个比较完善的前端MVW框架，包含模板，数据双向绑定，路由，模块化，服务，依赖注入等所有功能，模板功能强大丰富，并且是声明式的，自带了丰富的 Angular 指令。



## 说说你对闭包的理解



使用闭包主要是为了设计私有的方法和变量。闭包的优点是可以避免全局变量的污染，缺点是闭包会常驻内存，会增大内存使用量，使用不当很容易造成内存泄露。


闭包有三个特性：

>1.函数嵌套函数

>2.函数内部可以引用外部的参数和变量

>3.参数和变量不会被垃圾回收机制回收

 具体请看：[详解js闭包](http://segmentfault.com/a/1190000000652891)


## CSS 相关问题



 >`display:none`和`visibility:hidden`的区别？


     display:none  隐藏对应的元素，在文档布局中不再给它分配空间，它各边的元素会合拢，就当他从来不存在。

     visibility:hidden  隐藏对应的元素，但是在文档布局中仍保留原来的空间。



 >CSS中 `link` 和 `@import` 的区别是？

     (1) link属于HTML标签，而@import是CSS提供的;

     (2) 页面被加载的时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载;

     (3) import只在IE5以上才能识别，而link是HTML标签，无兼容问题;

     (4) link方式的样式的权重 高于@import的权重.



 >`position:absolute`和`float`属性的异同



 - 共同点：对内联元素设置`float`和`absolute`属性，可以让元素脱离文档流，并且可以设置其宽高。


 - 不同点：`float`仍会占据位置，`position`会覆盖文档流中的其他元素。



 >介绍一下box-sizing属性？


 `box-sizing`属性主要用来控制元素的盒模型的解析模式。默认值是`content-box`。


 - `content-box`：让元素维持W3C的标准盒模型。元素的宽度/高度由`border + padding + content`的宽度/高度决定，设置`width/height`属性指的是`content`部分的宽/高

 - `border-box`：让元素维持IE传统盒模型（IE6以下版本和IE6~7的怪异模式）。设置`width/height`属性指的是`border + padding + content`



 标准浏览器下，按照W3C规范对盒模型解析，一旦修改了元素的边框或内距，就会影响元素的盒子尺寸，就不得不重新计算元素的盒子尺寸，从而影响整个页面的布局。

 >CSS 选择符有哪些？哪些属性可以继承？优先级算法如何计算？ CSS3新增伪类有那些？

     1.id选择器（ # myid）

     2.类选择器（.myclassname）

     3.标签选择器（div, h1, p）

     4.相邻选择器（h1 + p）

     5.子选择器（ul > li）

     6.后代选择器（li a）

     7.通配符选择器（ * ）

     8.属性选择器（a[rel = "external"]）

     9.伪类选择器（a: hover, li:nth-child）


 **优先级为:**


 `!important >  id > class > tag `

 `important` 比 内联优先级高,但内联比 `id` 要高



 >CSS3新增伪类举例：

 ```
     p:first-of-type 选择属于其父元素的首个 <p> 元素的每个 <p> 元素。

     p:last-of-type  选择属于其父元素的最后 <p> 元素的每个 <p> 元素。

     p:only-of-type  选择属于其父元素唯一的 <p> 元素的每个 <p> 元素。

     p:only-child    选择属于其父元素的唯一子元素的每个 <p> 元素。

     p:nth-child(2)  选择属于其父元素的第二个子元素的每个 <p> 元素。

     :enabled  :disabled 控制表单控件的禁用状态。

     :checked        单选框或复选框被选中。
 ```

 >CSS3有哪些新特性？

     CSS3实现圆角（border-radius），阴影（box-shadow），

     对文字加特效（text-shadow、），线性渐变（gradient），旋转（transform）

     transform:rotate(9deg) scale(0.85,0.90) translate(0px,-30px) skew(-9deg,0deg);//旋转,缩放,定位,倾斜

     增加了更多的CSS选择器  多背景 rgba

     在CSS3中唯一引入的伪元素是::selection.

     媒体查询，多栏布局

     border-image

 CSS3中新增了一种盒模型计算方式：`box-sizing`。盒模型默认的值是`content-box`, 新增的值是`padding-box`和`border-box`，几种盒模型计算元素宽高的区别如下：

 #### content-box（默认）

 布局所占宽度Width：

```javascript
 Width = width + padding-left + padding-right + border-left + border-right
```

 布局所占高度Height:

```javascript
 Height = height + padding-top + padding-bottom + border-top + border-bottom

 padding-box
```

 布局所占宽度Width：

```javascript
 Width = width(包含padding-left + padding-right) + border-top + border-bottom
```

 布局所占高度Height:

```javascript
 Height = height(包含padding-top + padding-bottom) + border-top + border-bottom

 border-box
```

 布局所占宽度Width：

```javascript
 Width = width(包含padding-left + padding-right + border-left + border-right)
```

 布局所占高度Height:

```javascript
 Height = height(包含padding-top + padding-bottom + border-top + border-bottom)
```

 >对BFC规范的理解？

       BFC，块级格式化上下文，一个创建了新的BFC的盒子是独立布局的，盒子里面的子元素的样式不会影响到外面的元素。在同一个BFC中的两个毗邻的块级盒在垂直方向（和布局方向有关系）的margin会发生折叠。

     （W3C CSS 2.1 规范中的一个概念，它决定了元素如何对其内容进行布局，以及与其他元素的关系和相互作用。）


### 常见兼容性问题？


   png24位的图片在iE6浏览器上出现背景，解决方案是做成PNG8.也可以引用一段脚本处理.

   浏览器默认的margin和padding不同。解决方案是加一个全局的*{margin:0;padding:0;}来统一。

   IE6双边距bug:块属性标签float后，又有横行的margin情况下，在ie6显示margin比设置的大。

   浮动ie产生的双倍距离（IE6双边距问题：在IE6下，如果对元素设置了浮动，同时又设置了margin-left或margin-right，margin值会加倍。）

   #box{ float:left; width:10px; margin:0 0 0 100px;}

   这种情况之下IE会产生20px的距离，解决方案是在float的标签样式控制中加入
   _display:inline; 将其转化为行内属性。(_这个符号只有ie6会识别)

   渐进识别的方式，从总体中逐渐排除局部。


     首先，巧妙的使用“\9”这一标记，将IE游览器从所有情况中分离出来。

     接着，再次使用“+”将IE8和IE7、IE6分离开来，这样IE8已经独立识别。

     css

         .bb{

          background-color:#f1ee18;/*所有识别*/

         .background-color:#00deff\9; /*IE6、7、8识别*/

         +background-color:#a200ff;/*IE6、7识别*/

         _background-color:#1e0bd1;/*IE6识别*/

         }


   怪异模式问题：漏写DTD声明，Firefox仍然会按照标准模式来解析网页，但在IE中会触发
   怪异模式。为避免怪异模式给我们带来不必要的麻烦，最好养成书写DTD声明的好习惯。现在
   可以使用[html5](http://www.w3.org/TR/html5/single-page.html)推荐的写法：`<doctype html>`



>上下margin重合问题

   ie和ff都存在，相邻的两个div的margin-left和margin-right不会重合，但是margin-top和margin-bottom却会发生重合。

   解决方法，养成良好的代码编写习惯，同时采用margin-top或者同时采用margin-bottom。


### 解释下浮动和它的工作原理？清除浮动的技巧



   浮动元素脱离文档流，不占据空间。浮动元素碰到包含它的边框或者浮动元素的边框停留。


   1.使用空标签清除浮动。

      这种方法是在所有浮动标签后面添加一个空标签 定义css clear:both. 弊端就是增加了无意义标签。

   2.使用overflow。

      给包含浮动元素的父标签添加css属性 overflow:auto; zoom:1; zoom:1用于兼容IE6。

   3.使用after伪对象清除浮动。

      该方法只适用于非IE浏览器。具体写法可参照以下示例。使用中需注意以下几点。一、该方法中必须为需要清除浮动元素的伪对象中设置 height:0，否则该元素会比实际高出若干像素；



 ### 浮动元素引起的问题和解决办法？


     浮动元素引起的问题：

     （1）父元素的高度无法被撑开，影响与父元素同级的元素

     （2）与浮动元素同级的非浮动元素（内联元素）会跟随其后

     （3）若非第一个元素浮动，则该元素之前的元素也需要浮动，否则会影响页面显示的结构



 >解决方法：

 使用`CSS`中的`clear:both`;属性来清除元素的浮动可解决2、3问题，对于问题1，添加如下样式，给父元素添加`clearfix`样式：

```css
     .clearfix:after{content: ".";display: block;height: 0;clear: both;visibility: hidden;}

     .clearfix{display: inline-block;} /* for IE/Mac */
```

 **清除浮动的几种方法：**


     1. 额外标签法，<div style="clear:both;"></div>（缺点：不过这个办法会增加额外的标签使HTML结构看起来不够简洁。）

     2. 使用after伪类

     #parent:after{

         content:".";

         height:0;

         visibility:hidden;

         display:block;

         clear:both;

         }


     3. 浮动外部元素

     4. 设置overflow为hidden或者auto

### js对象的深度克隆

```javascript
       function clone(Obj) {

             var buf;

             if (Obj instanceof Array) {

                 buf = [];  //创建一个空的数组

                 var i = Obj.length;

                 while (i--) {

                     buf[i] = clone(Obj[i]);

                 }

                 return buf;

             }else if (Obj instanceof Object){

                 buf = {};  //创建一个空对象

                 for (var k in Obj) {  //为这个对象添加新的属性

                     buf[k] = clone(Obj[k]);

                 }

                 return buf;

             }else{

                 return Obj;

             }

         }
```

### 说说你对Promise的理解



 依照 `Promise/A+` 的定义，`Promise` 有四种状态：



 	pending: 初始状态, 非 fulfilled 或 rejected.

 	fulfilled: 成功的操作.

 	rejected: 失败的操作.

 	settled: Promise已被fulfilled或rejected，且不是pending



 另外， `fulfilled` 与 `rejected` 一起合称 `settled`。



 `Promise` 对象用来进行延迟(deferred) 和异步(asynchronous ) 计算。



 >Promise 的构造函数



 构造一个 `Promise`，最基本的用法如下：


```javascript
 	var promise = new Promise(function(resolve, reject) {

 	    if (...) {  // succeed

 	        resolve(result);

 	    } else {   // fails

 	        reject(Error(errMessage));

 	    }

 	});
```


 `Promise` 实例拥有 `then` 方法（具有 `then` 方法的对象，通常被称为 `thenable`）。它的使用方法如下：

```javascript
 promise.then(onFulfilled, onRejected)
```

 接收两个函数作为参数，一个在 `fulfilled` 的时候被调用，一个在 `rejected` 的时候被调用，接收参数就是 `future，onFulfilled` 对应 `resolve`, `onRejected` 对应 `reject`。
