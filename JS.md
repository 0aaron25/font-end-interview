## JS相关面试题

#### 1.common.js 和 es6 中模块引入的区别？

CommonJS 是一种模块规范，最初被应用于 Nodejs，成为 Nodejs 的模块规范。运行在浏览器端的 JavaScript 由于也缺少类似的规范，在 ES6 出来之前，前端也实现了一套相同的模块规范 (例如: AMD)，用来对前端模块进行管理。自 ES6 起，引入了一套新的 ES6 Module 规范，在语言标准的层面上实现了模块功能，而且实现得相当简单，有望成为浏览器和服务器通用的模块解决方案。但目前浏览器对 ES6 Module 兼容还不太好，我们平时在 Webpack 中使用的 export 和 import，会经过 Babel 转换为 CommonJS 规范。在使用上的差别主要有：

1. CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。
2. CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。
3. CommonJs 是单个值导出，ES6 Module可以导出多个
4. CommonJs 是动态语法可以写在判断里，ES6 Module 静态语法只能写在顶层
5. CommonJs 的 this 是当前模块，ES6 Module的 this 是 undefined

#### 2.如何判断 0.1 + 0.2 与 0.3 相等？

作为一道面试题，我觉得重要的是要讲出一点其他人一般不会答出来的深度。像这道题，可以从原理和解决方案两个地方作为答题点，最好在编一个案例。大致讲自己遇到过这个问题，于是很好奇深入研究了一下，发现是浮点数精度导致……原理怎样怎样……然后又看了业界的库的源码，然后怎样怎样解决。

关于原理，我专门写了一篇文章 [mqyqingfeng/Blog#155](https://github.com/mqyqingfeng/Blog/issues/155) 来解释，实际回答的时候，我觉得答出来

1. 非是 ECMAScript 独有
2. IEEE754 标准中 64 位的储存格式，比如 11 位存偏移值
3. 其中涉及的三次精度丢失

就已经 OK 了。

再讲解决方案，这个可以直接搜索到，各种方案都了解一下，比较一下优劣，还可以参考业界的一些库的实现，比如 math.js，不过相关的我并没有看过……

如果还有精力的话，可以从加法再拓展讲讲超出安全值的数字的计算问题。

所以我觉得一能回答出底层实现，二能回答出多种解决方案的优劣，三能拓展讲讲 bignum 的处理，就是一个非常不错的回答了。

#### 3.鼠标滚动的时候，会触发很多次事件，如何解决的？

这里选择的方法应该是节流，可以拓展讲到防抖和节流，防抖是指连续触发的时候只会执行一次，停止触发 N 秒后才能继续执行，而节流是指如果你持续触发事件，每隔一段时间，只执行一次事件。像防止按钮多次点击就用防抖，像是监听滚动事件就用节流，函数实现都可以参照 underscore 代码中的实现，以前我写过 [JavaScript专题之跟着underscore学防抖](https://github.com/mqyqingfeng/Blog/issues/22) 和 [JavaScript专题之跟着 underscore 学节流](https://github.com/mqyqingfeng/Blog/issues/26) 两篇文章讲述了 underscore 中的实现方式

#### 4.谈一下隐式类型转换

这个问题可以拓展讲成 JavaScript 中的类型转换，分为两类，显式类型转换和隐式类型转换，当我们用 Number() 等函数的时候，就是显式类型转换，其转换规则是当是基本类型时，参照规范中的对应表进行转换，当不是基本类型的时候，先参照规范中的 `ToPrimitive` 方法转换为基本类型，再按照对应表转换，当执行 ToPrimitive 的时候，又会根据情况不同，判断先执行对象的 valueOf 方法还是 toString 方法进行准换，这个可以参照 [JavaScript 深入之头疼的类型转换(上)](https://github.com/mqyqingfeng/Blog/issues/159)，而当我们进行运算的时候，经常发生的就是隐式类型转换，比如 `+` 和 `==` 运算符，当 + 运算符的时候，更倾向于转成字符串，而当 `==` 的时候，更倾向于转为数字，这个在 [JavaScript 深入之头疼的类型转换(下)](https://github.com/mqyqingfeng/frontend-interview-question-and-answer/issues/47)中会讲到……但是我还在写……总之，回答类型转换的时候，最好是扯到规范中，表明你在研究这块内容的时候，还专门去看过规范。基本上回答了这里，对类型转换说明已经有很多的了解，但你可以再拓展讲一下，比如当时我在学习类型转换的时候，还专门去研究了如何花式表示 26 个字母。

#### 5.说一下闭包

一句话可以概括:闭包就是能够读取其他函数内部变量的函数，或者子函数在外调用， 子函数所在的父函数的作用域不会被释放。

(1)什么是闭包:
 闭包是指有权访问另外一个函数作用域中的变量的函数。 闭包就是函数的局部变量集合，只是这些局部变量在函数返回后会继续存在。闭包就是 就是函数的“堆栈”在函数返回后并不释放，我们也可以理解为这些函数堆栈并不在栈 上分配而是在堆上分配。当在一个函数内定义另外一个函数就会产生闭包。

 (2)为什么要用: 匿名自执行函数:我们知道所有的变量，如果不加上 var 关键字，则默认的会添加到全 局对象的属性上去，这样的临时变量加入全局对象有很多坏处，比如:别的函数可能误 用这些变量;造成全局对象过于庞大，影响访问速度(因为变量的取值是需要从原型链 上遍历的)。除了每次使用变量都是用 var 关键字外，我们在实际情况下经常遇到这样一 种情况，即有的函数只需要执行一次，其内部变量无需维护，可以用闭包。 结果缓存:我们开发中会碰到很多情况，设想我们有一个处理过程很耗时的函数对象， 每次调用都会花费很长时间，那么我们就需要将计算出来的值存储起来，当调用这个函 数的时候，首先在缓存中查找，如果找不到，则进行计算，然后更新缓存并返回值，如 果找到了，直接返回查找到的值即可。闭包正是可以做到这一点，因为它不会释放外部 的引用，从而函数内部的值可以得以保留。
 封装:实现类和继承等。

#### 6.说一下类的创建和继承

##### (1)类的创建(es5):

new 一个 function，在这个 function 的 prototype 里面增加属性和 方法。
 下面来创建一个 Animal 类:

```javascript
 // 定义一个动物类
 function Animal (name) {
 // 属性
 this.name = name || 'Animal';
 // 实例方法
 this.sleep = function(){
 console.log(this.name + '正在睡觉!');
 }
 }
 // 原型方法
 Animal.prototype.eat = function(food) {
 console.log(this.name + '正在吃:' + food);
 };
```

 这样就生成了一个 Animal 类，实力化生成对象后，有方法和属性。

##### (2)类的继承——原型链继承

```javascript
--原型链继承
function Cat(){ }
Cat.prototype = new Animal();
Cat.prototype.name = 'cat';
// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.eat('fish'));
console.log(cat.sleep());
console.log(cat instanceof Animal); //true
console.log(cat instanceof Cat); //true
```

介绍:在这里我们可以看到 new 了一个空对象,这个空对象指向 Animal 并且 Cat.prototype 指向了这个空对象，这种就是基于原型链的继承。

 特点:基于原型链，既是父类的实例，也是子类的实例
 缺点:无法实现多继承

##### (3)构造继承:

使用父类的构造函数来增强子类实例，等于是复制父类的实例属性给 子类(没用到原型)

```javascript
function Cat(name){ Animal.call(this); this.name = name || 'Tom'; }
// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // false
console.log(cat instanceof Cat); // true
```

特点:可以实现多继承 缺点:只能继承父类实例的属性和方法，不能继承原型上的属性和方法。

##### (4)实例继承和拷贝继承

 实例继承:为父类实例添加新特性，作为子类实例返回 拷贝继承:拷贝父类元素上的属性和方法
 上述两个实用性不强，不一一举例。

##### (5)组合继承:

相当于构造继承和原型链继承的组合体。通过调用父类构造，继承父 类的属性并保留传参的优点，然后通过将父类实例作为子类原型，实现函数复用

```javascript
	function Cat(name){
Animal.call(this);
this.name = name || 'Tom';
}
Cat.prototype = new Animal();
Cat.prototype.constructor = Cat;
// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // true
console.log(cat instanceof Cat); // true
```

特点:可以继承实例属性/方法，也可以继承原型属性/方法 缺点:调用了两次父类构造函数，生成了两份实例

##### (6)寄生组合继承:

通过寄生方式，砍掉父类的实例属性，这样，在调用两次父类的 构造的时候，就不会初始化两次实例方法/属性

```javascript
function Cat(name){
Animal.call(this);
this.name = name || 'Tom';
}
(function(){
// 创建一个没有实例方法的类
var Super = function(){};
Super.prototype = Animal.prototype; //将实例作为子类的原型
Cat.prototype = new Super();
})();
// Test Code
var cat = new Cat(); console.log(cat.name); console.log(cat.sleep());
console.log(cat instanceof Animal); // true console.log(cat instanceof Cat); //true
```

#### 7.说说前端中的事件流

HTML 中与 javascript 交互是通过事件驱动来实现的，例如鼠标点击事件 onclick、页面 的滚动事件 onscroll 等等，可以向文档或者文档中的元素添加事件侦听器来预订事件。 想要知道这些事件是在什么时候进行调用的，就需要了解一下“事件流”的概念。 什么是事件流:事件流描述的是从页面中接收事件的顺序,DOM2 级事件流包括下面几个 阶段。
 事件捕获阶段
 处于目标阶段
 事件冒泡阶段
 addEventListener:addEventListener 是 DOM2 级事件新增的指定事件处理程序的操作， 这个方法接收 3 个参数:要处理的事件名、作为事件处理程序的函数和一个布尔值。最 后这个布尔值参数如果是 true，表示在捕获阶段调用事件处理程序;如果是 false，表示 在冒泡阶段调用事件处理程序。
 IE 只支持事件冒泡。

#### 8.如何让事件先冒泡后捕获

在 DOM 标准事件模型中，是先捕获后冒泡。但是如果要实现先冒泡后捕获的效果，对 于同一个事件，监听捕获和冒泡，分别对应相应的处理函数，监听到捕获事件，先暂缓 执行，直到冒泡事件被捕获后再执行捕获之间。

#### 9.说一下事件委托

简介:事件委托指的是，不在事件的发生地(直接 dom)上设置监听函数，而是在其父 元素上设置监听函数，通过事件冒泡，父元素可以监听到子元素上事件的触发，通过判 断事件发生元素 DOM 的类型，来做出不同的响应。
 举例:最经典的就是 ul 和 li 标签的事件监听，比如我们在添加事件时候，采用事件委 托机制，不会在 li 标签上直接添加，而是在 ul 父元素上添加。 好处:比较合适动态元素的绑定，新添加的子元素也会有监听函数，也可以有事件触发 机制。

#### 10.说一下图片的懒加载和预加载

预加载:提前加载图片，当用户需要查看时可直接从本地缓存中渲染。 懒加载:懒加载的主要目的是作为服务器前端的优化，减少请求数或延迟请求数。

两种技术的本质:两者的行为是相反的，一个是提前加载，一个是迟缓甚至不加载。 懒加载对服务器前端有一定的缓解压力作用，预加载则会增加服务器前端压力。

#### 11.JS 的 new 操作符做了哪些事情

new 操作符新建了一个空对象，这个对象原型指向构造函数的 prototype，执行构造函数 后返回这个对象。

#### 12.改变函数内部 this 指针的指向函数(bind，apply，call 的区别)

通过 apply 和 call 改变函数的 this 指向，他们两个函数的第一个参数都是一样的表示要 改变指向的那个对象，第二个参数，apply 是数组，而 call 则是 arg1,arg2...这种形式。通 过 bind 改变 this 作用域会返回一个新的函数，这个函数不会马上执行。

#### 13.JS 的各种位置，比如 clientHeight,scrollHeight,offsetHeight ,以及 scrollTop, offsetTop,clientTop 的区别?

clientHeight:表示的是可视区域的高度，不包含 border 和滚动条 offsetHeight:表示可视区域的高度，包含了 border 和滚动条 scrollHeight:表示了所有区域的高度，包含了因为滚动被隐藏的部分。 clientTop:表示边框 border 的厚度，在未指定的情况下一般为 0 scrollTop:滚动后被隐藏的高度，获取对象相对于由 offsetParent 属性指定的父坐标(css 定位的元素或 body 元素)距离顶端的高度

#### 14.异步加载 JS 的方法(defer和async的区别)

**defer**: 只支持 IE 如果您的脚本不会改变文档的内容，可将 defer 属性加入到<script>标 签中，以便加快处理文档的速度。因为浏览器知道它将能够安全地读取文档的剩余部分 而不用执行脚本，它将推迟对脚本的解释，直到文档已经显示给用户为止。

 **async**，HTML5 属性仅适用于外部脚本，并且如果在 IE 中，同时存在 defer 和 async，那 么 defer 的优先级比较高，脚本将在页面完成时执行。

创建 script 标签，插入到 DOM 中

#### 15.Ajax 解决浏览器缓存问题

在 ajax 发送请求前加上 anyAjaxObj.setRequestHeader("If-Modified-Since","0")。

在 ajax 发送请求前加上 anyAjaxObj.setRequestHeader("Cache-Control","no-cache")。

在 URL 后面加上一个随机数: "fresh=" + Math.random()。

在 URL 后面加上时间搓:"nowtime=" + new Date().getTime()。

#### 16.JS 的节流和防抖

参考：http://www.cnblogs.com/coco1s/p/5499469.html

#### 17.JS 中的垃圾回收机制

必要性:由于字符串、对象和数组没有固定大小，所有当他们的大小已知时，才能对他 们进行动态的存储分配。JavaScript 程序每次创建字符串、数组或对象时，解释器都必 须分配内存来存储那个实体。只要像这样动态地分配了内存，最终都要释放这些内存以 便他们能够被再用，否则，JavaScript 的解释器将会消耗完系统中所有可用的内存，造 成系统崩溃。
 这段话解释了为什么需要系统需要垃圾回收，JS 不像 C/C++，他有自己的一套垃圾回收 机制(Garbage Collection)。JavaScript 的解释器可以检测到何时程序不再使用一个对象 了，当他确定了一个对象是无用的时候，他就知道不再需要这个对象，可以把它所占用 的内存释放掉了。例如:

var a="hello world";
 var b="world";
 var a=b;
 //这时，会释放掉"hello world"，释放内存以便再引用 垃圾回收的方法:标记清除、计数引用。

标记清除 这是最常见的垃圾回收方式，当变量进入环境时，就标记这个变量为”进入环境“,从逻 辑上讲，永远不能释放进入环境的变量所占的内存，永远不能释放进入环境变量所占用 的内存，只要执行流程进入相应的环境，就可能用到他们。当离开环境时，就标记为离 开环境。 垃圾回收器在运行的时候会给存储在内存中的变量都加上标记(所有都加)，然后去掉 环境变量中的变量，以及被环境变量中的变量所引用的变量(条件性去除标记)，删除 所有被标记的变量，删除的变量无法在环境变量中被访问所以会被删除，最后垃圾回收 器，完成了内存的清除工作，并回收他们所占用的内存。
 引用计数法 另一种不太常见的方法就是引用计数法，引用计数法的意思就是每个值没引用的次数， 当声明了一个变量，并用一个引用类型的值赋值给改变量，则这个值的引用次数为 1,; 相反的，如果包含了对这个值引用的变量又取得了另外一个值，则原先的引用值引用次 数就减 1，当这个值的引用次数为 0 的时候，说明没有办法再访问这个值了，因此就把 所占的内存给回收进来，这样垃圾收集器再次运行的时候，就会释放引用次数为 0 的这 些值。
 用引用计数法会存在内存泄露，下面来看原因:
 function problem() {
 var objA = new Object();
 var objB = new Object();
 objA.someOtherObject = objB;
 objB.anotherObject = objA;
 }
 在这个例子里面，objA 和 objB 通过各自的属性相互引用，这样的话，两个对象的引用 次数都为 2，在采用引用计数的策略中，由于函数执行之后，这两个对象都离开了作用 域，函数执行完成之后，因为计数不为 0，这样的相互引用如果大量存在就会导致内存 泄露。
 特别是在 DOM 对象中，也容易存在这种问题:
 var element=document.getElementById(’‘);
 var myObj=new Object();
 myObj.element=element;
 element.someObject=myObj;
 这样就不会有垃圾回收的过程。

#### 18.如何理解前端模块化

前端模块化就是复杂的文件编程一个一个独立的模块，比如 JS 文件等等，分成独立的 模块有利于重用(复用性)和维护(版本迭代)，这样会引来模块之间相互依赖的问题， 所以有了 commonJS 规范，AMD，CMD 规范等等，以及用于 JS 打包(编译等处理)的 工具 webpack

#### 19.==和===、以及 Object.is 的区别

(1) ==
 主要存在:强制转换成 number,null==undefined " "==0 //true
 "0"==0 //true
 " " !="0" //true
 123=="123" //true
 null==undefined //true
 (2)Object.js
 主要的区别就是+0!=-0 而 NaN==NaN (相对比===和==的改进)

#### 20.setTimeout、setInterval 和 requestAnimationFrame 之间的区别

这里有一篇文章讲的是 requestAnimationFrame: http://www.cnblogs.com/xiaohuochai/p/5777186.html
 与 setTimeout 和 setInterval 不同，requestAnimationFrame 不需要设置时间间隔， 大多数电脑显示器的刷新频率是 60Hz，大概相当于每秒钟重绘 60 次。大多数浏览器都 会对重绘操作加以限制，不超过显示器的重绘频率，因为即使超过那个频率用户体验也 不会有提升。因此，最平滑动画的最佳循环间隔是 1000ms/60，约等于 16.6ms。
 RAF 采用的是系统时间间隔，不会因为前面的任务，不会影响 RAF，但是如果前面的 任务多的话，
 会响应 setTimeout 和 setInterval 真正运行时的时间间隔。
 特点:
 (1)requestAnimationFrame 会把每一帧中的所有 DOM 操作集中起来，在一次重绘或回 流中就完成，并且重绘或回流的时间间隔紧紧跟随浏览器的刷新频率。 (2)在隐藏或不可见的元素中，requestAnimationFrame 将不会进行重绘或回流，这当然 就意味着更少的 CPU、GPU 和内存使用量
 (3)requestAnimationFrame 是由浏览器专门为动画提供的 API，在运行时浏览器会自动 优化方法的调用，并且如果页面不是激活状态下的话，动画会自动暂停，有效节省了 CPU 开销。

#### 21 JS 怎么控制一次加载一张图片，加载完后再加载下一张

(1)方法 1
```html
 <script type="text/javascript">
 var obj=new Image();
  obj.src="http://www.phpernote.com/uploadfiles/editor/201107240502201179.jpg"; 
   obj.onload=function(){ 
     alert('图片的宽度为:'+obj.width+';图片的高度为:'+obj.height);
     document.getElementById("mypic").innnerHTML="<img src='"+this.src+"' />";
 }
 </script>
 <div id="mypic">onloading......</div>
```

 (2)方法 2
```html
 <script type="text/javascript">
 var obj=new Image();
   obj.src="http://www.phpernote.com/uploadfiles/editor/201107240502201179.jpg"; obj.onreadystatechange=function(){
 if(this.readyState=="complete"){
   alert('图片的宽度为:'+obj.width+';图片的高度为:'+obj.height);
	document.getElementById("mypic").innnerHTML="<img src='"+this.src+"' />"; }
}
</script>
<div id="mypic">onloading......</div>
```

#### 22.代码的执行顺序

```javascript
setTimeout(function(){
  console.log(1)},0); 
new Promise(function(resolve,reject){
  console.log(2);
		resolve();
}).then(function(){console.log(3) }).then(function(){console.log(4)}); 
process.nextTick(function(){console.log(5)});
console.log(6);
//输出 2,6,5,3,4,1
```

参考：https://github.com/forthealllight/blog/issues/5

#### 23.如何实现 sleep 的效果(es5 或者 es6)

##### (1)while 循环的方式

```javascript
function sleep(ms){
var start=Date.now(),expire=start+ms;
while(Date.now()<expire);
console.log('1111');
return;
}
```

执行 sleep(1000)之后，休眠了 1000ms 之后输出了 1111。上述循环的方式缺点很明显， 容易造成死循环。

##### (2)通过 promise 来实现

```javascript
function sleep(ms){
var temple=new Promise(
(resolve)=>{
console.log(111);setTimeout(resolve,ms)
});
return temple
}
sleep(500).then(function(){
  //console.log(222)
})
//先输出了 111，延迟 500ms 后输出 222
```

##### (3)通过 async 封装

```javascript
function sleep(ms){
return new Promise((resolve)=>setTimeout(resolve,ms));
}
async function test(){
var temple=await sleep(1000);
console.log(1111)
return temple
}
test();
//延迟 1000ms 输出了 1111
```

#### 24.Function._proto_(getPrototypeOf)是什么?

获取一个对象的原型，在 chrome 中可以通过_proto_的形式，或者在 ES6 中可以通过 Object.getPrototypeOf 的形式。
 那么 Function.proto 是什么么?也就是说 Function 由什么对象继承而来，我们来做如下判 别。
 Function.__proto__==Object.prototype //false
 Function.__proto__==Function.prototype//true
 我们发现 Function 的原型也是 Function。
 我们用图可以来明确这个关系:

![](/Users/liangjiahao/Pictures/截图图库/42493275-f55d0860-844e-11e8-983f-e04189a4f3d8.png)

#### 25.箭头函数中 this 指向举例

var a=11;
 function test2(){
 this.a=22;
 let b=()=>{console.log(this.a)} b();
 }
 var x=new test2();
 //输出 22
 定义时绑定

箭头函数与普通函数的区别在于:
 1、箭头函数没有 this，所以需要通过查找作用域链来确定 this 的值，这就意味着如果箭 头函数被非箭头函数包含，this 绑定的就是最近一层非箭头函数的 this， 2、箭头函数没有自己的 arguments 对象，但是可以访问外围函数的 arguments 对象 3、不能通过 new 关键字调用，同样也没有 new.target 值和原型

#### 26.JS 判断类型 

判断方法:typeof()，instanceof，Object.prototype.toString.call()等

#### 27.JS 实现跨域

跨域，是指浏览器不能执行其他网站的脚本。它是由浏览器的同源策略造成的，是浏览 器对 JavaScript 实施的安全限制，那么只要协议、域名、端口有任何一个不同，都被当 作是不同的域。跨域原理，即是通过各种方式，避开浏览器的安全限制。

JSONP:通过动态创建 script，再请求一个带参网址实现跨域通信。document.domain + iframe 跨域:两个页面都通过 js 强制设置 document.domain 为基础主域，就实现了同域。 location.hash + iframe 跨域:a 欲与 b 跨域相互通信，通过中间页 c 来实现。 三个页面， 不同域之间利用 iframe 的 location.hash 传值，相同域之间直接 js 访问来通信。 window.name + iframe 跨域:通过 iframe 的 src 属性由外域转向本地域，跨域数据即由 iframe 的 window.name 从外域传递到本地域。
 postMessage 跨域:可以跨域操作的 window 属性之一。
 CORS:服务端设置 Access-Control-Allow-Origin 即可，前端无须设置，若要带 cookie 请 求，前后端都需要设置。
 代理跨域:启一个代理服务器，实现数据的转发

#### 28.JS 基本数据类型

基本数据类型:undefined、null、number、boolean、string、symbol

#### 29.不同数据类型的值的比较，是怎么转换的，有什么规则

![](/Users/liangjiahao/Pictures/截图图库/截屏2022-03-15 22.22.18.png)

#### 30.this 的指向 哪几种

默认绑定:全局环境中，this 默认绑定到 window。 隐式绑定:一般地，被直接对象所包含的函数调用时，也称为方法调用，this 隐式绑定 到该直接对象。 隐式丢失:隐式丢失是指被隐式绑定的函数丢失绑定对象，从而默认绑定到 window。显 式绑定:通过 call()、apply()、bind()方法把对象绑定到 this 上，叫做显式绑定。
 new 绑定:如果函数或者方法调用之前带有关键字 new，它就构成构造函数调用。对于 this 绑定来说，称为 new 绑定。
 【1】构造函数通常不使用 return 关键字，它们通常初始化新对象，当构造函数的函数 体执行完毕时，它会显式返回。在这种情况下，构造函数调用表达式的计算结果就是这 个新对象的值。
 【2】如果构造函数使用 return 语句但没有指定返回值，或者返回一个原始值，那么这 时将忽略返回值，同时使用这个新对象作为调用结果。 

【3】如果构造函数显式地使用 return 语句返回一个对象，那么调用表达式的值就是这 个对象。

#### 31.暂停死区

在代码块内，使用 let、const 命令声明变量之前，该变量都是不可用的。这在语法上， 称为“暂时性死区”

#### 32.什么是按需加载

当用户触发了动作时才加载对应的功能。触发的动作，是要看具体的业务场景而言，包 括但不限于以下几个情况:鼠标点击、输入文字、拉动滚动条，鼠标移动、窗口大小更 改等。加载的文件，可以是 JS、图片、CSS、HTML 等。

#### 33.JS 中继承实现的几种方式

1、原型链继承，将父类的实例作为子类的原型，他的特点是实例是子类的实例也是父 类的实例，父类新增的原型方法/属性，子类都能够访问，并且原型链继承简单易于实 现，缺点是来自原型对象的所有属性被所有实例共享，无法实现多继承，无法向父类构 造函数传参。 2、构造继承，使用父类的构造函数来增强子类实例，即复制父类的实例属性给子类， 构造继承可以向父类传递参数，可以实现多继承，通过 call 多个父类对象。但是构造继 承只能继承父类的实例属性和方法，不能继承原型属性和方法，无法实现函数服用，每 个子类都有父类实例函数的副本，影响性能 

3、实例继承，为父类实例添加新特性，作为子类实例返回，实例继承的特点是不限制 调用方法，不管是 new 子类()还是子类()返回的对象具有相同的效果，缺点是实 例是父类的实例，不是子类的实例，不支持多继承 

4、拷贝继承:特点:支持多继承，缺点:效率较低，内存占用高(因为要拷贝父类的 属性)无法获取父类不可枚举的方法(不可枚举方法，不能使用 for in 访问到)

 5、组合继承:通过调用父类构造，继承父类的属性并保留传参的优点，然后通过将父 类实例作为子类原型，实现函数复用

 6、寄生组合继承:通过寄生方式，砍掉父类的实例属性，这样，在调用两次父类的构 造的时候，就不会初始化两次实例方法/属性，避免的组合继承的缺点

#### 34.简单介绍一下 symbol

Symbol 是 ES6 的新增属性，代表用给定名称作为唯一标识，这种类型的值可以这样创 建，let id=symbol(“id”)

Symbl 确保唯一，即使采用相同的名称，也会产生不同的值，我们创建一个字段，仅为 知道对应 symbol 的人能访问，使用 symbol 很有用，symbol 并不是 100%隐藏，有内置方 法 Object.getOwnPropertySymbols(obj)可以获得所有的 symbol。
 也有一个方法 Reflect.ownKeys(obj)返回对象所有的键，包括 symbol。 所以并不是真正隐藏。但大多数库内置方法和语法结构遵循通用约定他们是隐藏的。

#### 35.什么是事件监听

addEventListener()方法，用于向指定元素添加事件句柄，它可以更简单的控制事件，语 法为
 element.addEventListener(event, function, useCapture);
 第一个参数是事件的类型(如 "click" 或 "mousedown"). 第二个参数是事件触发后调用的函数。 第三个参数是个布尔值用于描述事件是冒泡还是捕获。该参数是可选的。 事件传递有两种方式，冒泡和捕获
 事件传递定义了元素事件触发的顺序，如果你将 P 元素插入到 div 元素中，用户点击 P 元素，
 在冒泡中，内部元素先被触发，然后再触发外部元素， 捕获中，外部元素先被触发，在触发内部元素。

#### 36.介绍一下 promise，及其底层如何实现

Promise 是一个对象，保存着未来将要结束的事件，她有两个特征: 1、对象的状态不受外部影响，Promise 对象代表一个异步操作，有三种状态，pending 进行中，fulfilled 已成功，rejected 已失败，只有异步操作的结果，才可以决定当前是哪 一种状态，任何其他操作都无法改变这个状态，这也就是 promise 名字的由来 2、一旦状态改变，就不会再变，promise 对象状态改变只有两种可能，从 pending 改到 fulfilled 或者从 pending 改到 rejected，只要这两种情况发生，状态就凝固了，不会再改 变，这个时候就称为定型 resolved,

```javascript
//Promise 的基本用法
let promise1 = new Promise(function(resolve,reject){
setTimeout(function(){
resolve('ok')
},1000)
})
promise1.then(function success(val){
console.log(val)
})
//最简单代码实现 promise
class PromiseM {
constructor (process) {

this.status = 'pending'
this.msg = ''
process(this.resolve.bind(this), this.reject.bind(this)) return this
}
resolve (val) {
this.status = 'fulfilled'
this.msg = val
}
reject (err) {
this.status = 'rejected'
this.msg = err
}
then (fufilled, reject) {
if(this.status === 'fulfilled') {
fufilled(this.msg)
}
if(this.status === 'rejected') {
reject(this.msg)
}
}
}
//测试代码
var mm=new PromiseM(function(resolve,reject){ resolve('123');
});
mm.then(function(success){
console.log(success);
},function(){
console.log('fail!');
});
```

#### 37.JS 原型链，原型链的顶端是什么?Object 的原型是什么?Object 的原型的 原型是什么?在数组原型链上实现删除数组重复数据的方法

能够把这个讲清楚弄明白是一件很困难的事，
 首先明白原型是什么，在 ES6 之前，JS 没有类和继承的概念，JS 是通过原型来实现继 承的，在 JS 中一个构造函数默认带有一个 prototype 属性，这个的属性值是一个对象， 同时这个 prototype 对象自带有一个 constructor 属性，这个属性指向这个构造函数，同时 每一个实例都会有一个_proto_属性指向这个 prototype 对象，我们可以把这个叫做隐式原 型，我们在使用一个实例的方法的时候，会先检查这个实例中是否有这个方法，没有的 话就会检查这个 prototype 对象是否有这个方法， 基于这个规则，如果让原型对象指向另一个类型的实例，即 constructor1.protoytpe=instance2，这时候如果试图引用 constructor1 构造的实例 instance1 的某个属性 p1,
 首先会在 instance1 内部属性中找一遍，接着会在 instance1._proto_(constructor1.prototype)即是 instance2 中寻找 p1 搜寻轨迹:instance1->instance2->constructor2.prototype......->Object.prototype;这即是原 型链，原型链顶端是 Object.prototype
 补充学习:

每个函数都有一个 prototype 属性，这个属性指向了一个对象，这个对象正是调用该函数 而创建的实例的原型，那么什么是原型呢，可以这样理解，每一个 JavaScript 对象在创 建的时候就会预制管理另一个对象，这个对象就是我们所说的原型，每一个对象都会从 原型继承属性，如图:

![](/Users/liangjiahao/Pictures/截图图库/截屏2022-03-15 22.36.20.png)



那么怎么表示实例与实例原型的关系呢，这时候就要用到第二个属性_proto_ 这是每一个 JS 对象都会有的一个属性，指向这个对象的原型，如图:

![](/Users/liangjiahao/Pictures/截图图库/截屏2022-03-15 22.36.49.png)



既然实例对象和构造函数都可以指向原型，那么原型是否有属性指向构造函数或者实例 呢，指向实例是没有的，因为一个构造函数可以生成多个实例，但是原型有属性可以直 接指向构造函数，通过 constructor 即可
 接下来讲解实例和原型的关系: 当读取实例的属性时，如果找不到，就会查找与对象相关的原型中的属性，如果还查不 到，就去找原型的原型，一直找到最顶层，那么原型的原型是什么呢，首先，原型也是 一个对象，既然是对象，我们就可以通过构造函数的方式创建它，所以原型对象就是通 过 Object 构造函数生成的，如图:

![](/Users/liangjiahao/Pictures/截图图库/截屏2022-03-15 22.37.27.png)

那么 Object.prototype 的原型呢，我们可以打印 console.log(Object.prototype.__proto__ === null)，返回 true
 null 表示没有对象，即该处不应有值，所以 Object.prototype 没有原型，如图:

![](/Users/liangjiahao/Pictures/截图图库/截屏2022-03-15 22.37.57.png)



图中这条蓝色的线即是原型链， 最后补充三点:
 constructor:
 function Person(){

}
 var person = new Person();
 console.log(Person === person.constructor);
 原本 person 中没有 constructor 属性，当不能读取到 constructor 属性时，会从 person 的原 型中读取，所以指向构造函数 Person
 __proto__:
 绝大部分浏览器支持这个非标准的方法访问原型，然而它并不存在与 Person.prototype 中， 实际上它来自 Object.prototype，当使用 obj.__proto__时，可以理解为返回来 Object.getPrototype(obj)
 继承:
 前面说到，每个对象都会从原型继承属性，但是引用《你不知道的 JS》中的话，继承意 味着复制操作，然而 JS 默认不会复制对象的属性，相反，JS 只是在两个对象之间创建 一个关联，这样子一个对象就可以通过委托访问另一个对象的属性和函数，所以与其叫 继承，叫委托更合适。

#### 38.事件委托以及冒泡原理

事件委托是利用冒泡阶段的运行机制来实现的，就是把一个元素响应事件的函数委托到 另一个元素，一般是把一组元素的事件委托到他的父元素上，委托的优点是 减少内存消耗，节约效率
 动态绑定事件
 事件冒泡，就是元素自身的事件被触发后，如果父元素有相同的事件，如 onclick 事件， 那么元素本身的触发状态就会传递，也就是冒到父元素，父元素的相同事件也会一级一 级根据嵌套关系向外触发，直到 document/window，冒泡过程结束。

#### 39.JS 中 string 的 startwith 和 indexof 两种方法的区别

JS 中 startwith 函数，其参数有 3 个，stringObj,要搜索的字符串对象，str，搜索的字符串， position，可选，从哪个位置开始搜索，如果以 position 开始的字符串以搜索字符串开头， 则返回 true，否则返回 false
 Indexof 函数，indexof 函数可返回某个指定字符串在字符串中首次出现的位置。

#### 40.有了解过事件模型吗，DOM0 级和 DOM2 级有什么区别，DOM 的分级是 什么

JSDOM 事件流存在如下三个阶段:
 事件捕获阶段
 处于目标阶段
 事件冒泡阶段
 JSDOM 标准事件流的触发的先后顺序为:先捕获再冒泡，点击 DOM 节点时，事件传播 顺序:事件捕获阶段，从上往下传播，然后到达事件目标节点，最后是冒泡阶段，从下 往上传播
 DOM 节点添加事件监听方法 addEventListener，中参数 capture 可以指定该监听是添加在 事件捕获阶段还是事件冒泡阶段，为 false 是事件冒泡，为 true 是事件捕获，并非所有 的事件都支持冒泡，比如 focus，blur 等等，我们可以通过 event.bubbles 来判断 事件模型有三个常用方法: event.stopPropagation:阻止捕获和冒泡阶段中，当前事件的进一步传播， event.stopImmediatePropagetion，阻止调用相同事件的其他侦听器， event.preventDefault，取消该事件(假如事件是可取消的)而不停止事件的进一步传播， event.target:指向触发事件的元素，在事件冒泡过程中这个值不变
 event.currentTarget = this，时间帮顶的当前元素，只有被点击时目标元素的 target 才会等 于 currentTarget，
 最后，对于执行顺序的问题，如果 DOM 节点同时绑定了两个事件监听函数，一个用于 捕获，一个用于冒泡，那么两个事件的执行顺序真的是先捕获在冒泡吗，答案是否定的， 绑定在被点击元素的事件是按照代码添加顺序执行的，其他函数是先捕获再冒泡

#### 41.JS 的垃圾回收机制

GC(garbage collection)，GC 执行时，中断代码，停止其他操作，遍历所有对象，对于 不可访问的对象进行回收，在 V8 引擎中使用两种优化方法，
 分代回收，2、增量 GC，目的是通过对象的使用频率，存在时长来区分新生代和老生代 对象，多回收新生代区，少回收老生代区，减少每次遍历的时间，从而减少 GC 的耗时 回收方法: 引用计次，当对象被引用的次数为零时进行回收，但是循环引用时，两个对象都至少被 引用了一次，因此导致内存泄漏，
 标记清除

#### 42.怎么获得对象上的属性:比如说通过 Object.key()

从 ES5 开始，有三种方法可以列出对象的属性
 for(let I in obj)该方法依次访问一个对象及其原型链中所有可枚举的类型 object.keys:返回一个数组，包括所有可枚举的属性名称 object.getOwnPropertyNames:返回一个数组包含不可枚举的属性

#### 43.简单讲一讲 ES6 的一些新特性

ES6 在变量的声明和定义方面增加了 let、const 声明变量，有局部变量的概念，赋值中 有比较吸引人的结构赋值，同时 ES6 对字符串、 数组、正则、对象、函数等拓展了一 些方法，如字符串方面的模板字符串、函数方面的默认参数、对象方面属性的简洁表达 方式，ES6 也 引入了新的数据类型 symbol，新的数据结构 set 和 map,symbol 可以通过 typeof 检测出来，为解决异步回调问题，引入了 promise 和 generator，还有最为吸引人 了实现 Class 和模块，通过 Class 可以更好的面向对象编程，使用模块加载方便模块化编 程，当然考虑到 浏览器兼容性，我们在实际开发中需要使用 babel 进行编译 重要的特性:
 块级作用域:ES5 只有全局作用域和函数作用域，块级作用域的好处是不再需要立即执 行的函数表达式，循环体中的闭包不再有问题
 rest 参数:用于获取函数的多余参数，这样就不需要使用 arguments 对象了， promise:一种异步编程的解决方案，比传统的解决方案回调函数和事件更合理强大 模块化:其模块功能主要有两个命令构成，export 和 import，export 命令用于规定模块的 对外接口，import 命令用于输入其他模块提供的功能

#### 44.call 和 apply 是用来做什么

Call 和 apply 的作用是一模一样的，只是传参的形式有区别而已 1、改变 this 的指向
 2、借用别的对象的方法，
 3、调用函数，因为 apply，call 方法会使函数立即执行

#### 45.JavaScript 中的轮播实现原理?假如一个页面上有两个轮播，你会怎么实现?

图片轮播的原理就是图片排成一行，然后准备一个只有一张图片大小的容器，对这个容 器设置超出部分隐藏，在控制定时器来让这些图片整体左移或右移，这样呈现出来的效 果就是图片在轮播了。
 如果有两个轮播，可封装一个轮播组件，供两处调用

#### 46.事件代理

事件代理是利用事件的冒泡原理来实现的，何为事件冒泡呢?就是事件从最深的节点开 始，然后逐步向上传播事件，举个例子:页面上有这么一个节点树，div>ul>li>a;比如给 最里面的 a 加一个 click 点击事件，那么这个事件就会一层一层的往外执行，执行顺序 a>li>ul>div，有这样一个机制，那么我们给最外面的 div 加点击事件，那么里面的 ul，li， a 做点击事件的时候，都会冒泡到最外层的 div 上，所以都会触发，这就是事件代理， 代理它们父级代为执行事件。

#### 47.Eventloop

任务队列中，在每一次事件循环中，macrotask 只会提取一个执行，而 microtask 会一直 提取，直到 microsoft 队列为空为止。
 也就是说如果某个 microtask 任务被推入到执行中，那么当主线程任务执行完成后，会 循环调用该队列任务中的下一个任务来执行，直到该任务队列到最后一个任务为止。而 事件循环每次只会入栈一个 macrotask,主线程执行完成该任务后又会检查 microtasks 队 列并完成里面的所有任务后再执行 macrotask 的任务。macrotasks: setTimeout, setInterval, setImmediate, I/O, UI rendering
 microtasks: process.nextTick, Promise, MutationObserver

#### 48.ajax 返回的状态

0 - (未初始化)还没有调用 send()方法
 1 - (载入)已调用 send()方法，正在发送请求
 2 - (载入完成)send()方法执行完成，已经接收到全部响应内容

3 - (交互)正在解析响应内容
 4 - (完成)响应内容解析完成，可以在客户端调用了

#### 49.知道PWA吗

PWA 全称 Progressive Web App，即渐进式 WEB 应用。一个 PWA 应用首先是一个网页, 可以通过 Web 技术编写出一个网页应用. 随后添加上 App Manifest 和 Service Worker 来实现 PWA 的安装和离线等功能