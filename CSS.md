## CSS相关

#### 1.如何画一个三角形

```css
//三角形原理:边框的均分原理
div {
width:0px;
height:0px;
border-top:10px solid red; border-right:10px solid transparent; border-bottom:10px solid transparent; border-left:10px solid transparent;
}
```

#### 2.CSS3 加了什么属性？

css3:
 CSS3 边框如 border-radius，box-shadow 等;CSS3 背景如 background-size，background-origin 等;CSS3 2D，3D 转换如 transform 等;CSS3 动画如 animation 等。 参考 https://www.cnblogs.com/xkweb/p/5862612.html

CSS3 的新特性中，在布局方面新增了 flex 布局，在选择器方面新增了例如 first-of-type,nth-child 等选择器，在盒模型方面添加了 box-sizing 来改变盒模型，在动画 方面增加了 animation，2d 变换，3d 变换等，在颜色方面添加透明，rbga 等，在字体方 面允许嵌入字体和设置字体阴影，最后还有媒体查讯等

#### 3.说一下 css 盒模型

简介:就是用来装页面上的元素的矩形区域。CSS 中的盒子模型包括 IE 盒子模型和标准的 W3C 盒子模型。
 设置盒模型box-sizing(有 3 个值哦):border-box,padding-box,content-box.

CSS 盒模型本质上是一个盒子，封装周围的 HTML 元素，它包括:边距，边框，填充， 和实际内容。 

标准盒模型:一个块的总宽度=width+margin(左右)+padding(左右)+border(左右) 

怪异盒模型:一个块的总宽度=width+margin(左右)(既 width 已经包含了 padding 和 border 值)


 **标准盒子模型:**

![](/Users/liangjiahao/Pictures/截图图库/截屏2022-03-15 19.45.22.png)			 	

**IE 盒子模型:**

![](/Users/liangjiahao/Pictures/截图图库/截屏2022-03-15 19.46.04.png)

区别:从图中我们可以看出，这两种盒子模型最主要的区别就是 width 的包含范围，在 标准的盒子模型中，width 指 content 部分的宽度，在 IE 盒子模型中，width 表示 content+padding+border 这三个部分的宽度，故这使得在计算整个盒子的宽度时存在着差异:标准盒子模型的盒子宽度:左右 border+左右 padding+width  IE 盒子模型的盒子宽度:width
 在 CSS3 中引入了 box-sizing 属性，box-sizing:content-box;表示标准的盒子模型， box-sizing:border-box 表示的是 IE 盒子模型 最后，前面我们还提到了，box-sizing:padding-box,这个属性值的宽度包含了左右 padding+width
 也很好理解性记忆，包含什么，width 就从什么开始算起。

#### 4.画一条 0.5px 的线

采用 meta viewport 的方式
 <meta name="viewport" content="initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />

采用 border-image 的方式 

采用 transform: scale()的方式

#### 5.link 标签和 import 标签的区别

link 属于 html 标签，而@import 是 css 提供的
 页面被加载时，link 会同时被加载，而@import 引用的 css 会等到页面加载结束后加载。 link 是 html 标签，因此没有兼容性，而@import 只有 IE5 以上才能识别。
 link 方式样式的权重高于@import 的。

#### 6.transition 和 animation 的区别

Animation 和 transition 大部分属性是相同的，他们都是随时间改变元素的属性值，他们 的主要区别是 transition 需要触发一个事件才能改变属性，而 animation 不需要触发任何 事件的情况下才会随时间改变属性值，并且 transition 为 2 帧，从 from .... to，而 animation 可以一帧一帧的

#### 7.Flex 布局

文章链接: http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool(语法篇) http://www.ruanyifeng.com/blog/2015/07/flex-examples.html(实例篇)

Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。 布局的传统解决方案，基于盒状模型，依赖 display 属性 + position 属性 + float 属性。它 对于那些特殊布局非常不方便，比如，垂直居中就不容易实现。 简单的分为容器属性和元素属性
 容器的属性:
 flex-direction:决定主轴的方向(即子 item 的排列方法)
 .box {
 flex-direction: row | row-reverse | column | column-reverse;
 }
 flex-wrap:决定换行规则
 .box{
 flex-wrap: nowrap | wrap | wrap-reverse;
 }
 flex-flow:
 .box {
 flex-flow: <flex-direction> || <flex-wrap>;
 }
 justify-content:对其方式，水平主轴对齐方式
 align-items:对齐方式，竖直轴线方向
 项目的属性(元素的属性):
 order 属性:定义项目的排列顺序，顺序越小，排列越靠前，默认为 0
 flex-grow 属性:定义项目的放大比例，即使存在空间，也不会放大

flex-shrink 属性:定义了项目的缩小比例，当空间不足的情况下会等比例的缩小，如果 定义个 item 的 flow-shrink 为 0，则为不缩小
 flex-basis 属性:定义了在分配多余的空间，项目占据的空间。
 flex:是 flex-grow 和 flex-shrink、flex-basis 的简写，默认值为 0 1 auto 后两个属性 可选。 align-self:允许单个项目与其他项目不一样的对齐方式，可以覆盖 align-items，默认属 性为 auto，表示继承父元素的 align-items 比如说，用 flex 实现圣杯布局

#### 8.BFC(块级格式化上下文，用于清楚浮动，防止 margin 重叠等)

直译成:块级格式化上下文，是一个独立的渲染区域，并且有一定的布局规则。 BFC 区域不会与 float box 重叠
 BFC 是页面上的一个独立容器，子元素不会影响到外面
 计算 BFC 的高度时，浮动元素也会参与计算
 那些元素会生成 BFC:
 根元素
 float 不为 none 的元素
 position 为 fixed 和 absolute 的元素
 display 为 inline-block、table-cell、table-caption，flex，inline-flex 的元素 overflow 不为 visible 的元素

#### 9.垂直居中的方法

##### 1.margin:auto 法

```css
 div{
 width: 400px;
 height: 400px;
 position: relative;
 border: 1px solid #465468; }
 img{
 position: absolute;
 margin: auto;
 top: 0;
 left: 0;
 right: 0;
 bottom: 0;
 }
```

```html
<div> <img src="mm.jpg">  </div>
```

  定位为上下左右为 0，margin:0 可以实现脱离文档流的居中.

##### 2.margin 负值法

```css
.container{
width: 500px;
height: 400px;
border: 2px solid #379;
position: relative;
}
.inner{
width: 480px;
height: 380px;
background-color: #746;
position: absolute;
top: 50%;
left: 50%;
margin-top: -190px; /*height 的一半*/
margin-left: -240px; /*width 的一半*/
}
```

补充:其实这里也可以将 marin-top 和 margin-left 负值替换成， transform:translateX(-50%)和 transform:translateY(-50%)

##### 3.利用 flex

将父元素设置为 display:flex，并且设置 align-items:center;justify-content:center;



父元素固定宽高，利用定位及设置子元素 margin 值为自身的一半。

 父元素固定宽高，子元素设置 position: absolute，margin:auto 平均分配 margin css3 属性 transform。子元素设置 position: absolute; left: 50%; top: 50%;transform: translate(-50%,-50%);即可。
 将父元素设置成 display: table, 子元素设置为单元格 display: table-cell。 弹性布局 display: flex。设置 align-items: center; justify-content: center;

#### 10.关于 JS 动画和 css3 动画的差异性

渲染线程分为 main thread 和 compositor thread，如果 css 动画只改变 transform 和 opacity， 这时整个 CSS 动画得以在 compositor trhead 完成(而 JS 动画则会在 main thread 执行，然 后出发 compositor thread 进行下一步操作)，特别注意的是如果改变 transform 和 opacity 是不会 layout 或者 paint 的。
 区别:
 功能涵盖面，JS 比 CSS 大
 实现/重构难度不一，CSS3 比 JS 更加简单，性能跳优方向固定 对帧速表现不好的低版本浏览器，css3 可以做到自然降级
 css 动画有天然事件支持
 css3 有兼容性问题

#### 11.说一下块元素和行元素

块元素:独占一行，并且有自动填满父元素，可以设置 margin 和 pading 以及高度和宽 度
行元素:不会独占一行，width 和 height 会失效，并且在垂直方向的 padding 和 margin 会失效。

#### 12.多行元素的文本省略号

```css
display: -webkit-box 
-webkit-box-orient:vertical
-webkit-line-clamp:3
overflow:hidden
```

#### 13.visibility=hidden, opacity=0，display:none区别

opacity=0，该元素隐藏起来了，但不会改变页面布局，并且，如果该元素已经绑定一些 事件，如 click 事件，那么点击该区域，也能触发点击事件的 visibility=hidden，该元素 隐藏起来了，但不会改变页面布局，但是不会触发该元素已经绑定的事件 display=none， 把元素隐藏起来，并且会改变页面布局，可以理解成在页面中把该元素删除掉一样。

#### 14.双边距重叠问题(外边距折叠)

多个相邻(兄弟或者父子关系)普通流的块元素垂直方向 marigin 会重叠 折叠的结果为: 两个相邻的外边距都是正数时，折叠结果是它们两者之间较大的值。 两个相邻的外边距都是负数时，折叠结果是两者绝对值的较大值。 两个外边距一正一负时，折叠结果是两者的相加的和。

#### 15.position 属性 比较

##### 1.固定定位 fixed: 

元素的位置相对于浏览器窗口是固定位置，即使窗口是滚动的它也不会移动。Fixed 定 位使元素的位置与文档流无关，因此不占据空间。 Fixed 定位的元素和其他元素重叠。 

##### 2.相对定位 relative:

 如果对一个元素进行相对定位，它将出现在它所在的位置上。然后，可以通过设置垂直 或水平位置，让这个元素“相对于”它的起点进行移动。 在使用相对定位时，无论是 否进行移动，元素仍然占据原来的空间。因此，移动元素会导致它覆盖其它框。 

##### 3.绝对定位 absolute:

 绝对定位的元素的位置相对于最近的已定位父元素，如果元素没有已定位的父元素，那 么它的位置相对于<html>。absolute 定位使元素的位置与文档流无关，因此不占据空间。 absolute 定位的元素和其他元素重叠。

##### 4.粘性定位 sticky:

元素先按照普通文档流定位，然后相对于该元素在流中的 flow root(BFC)和 containing block(最近的块级祖先元素)定位。而后，元素定位表现为在跨越特定阈值前为相对定 位，之后为固定定位。

##### 5.默认定位 Static:

默认值。没有定位，元素出现在正常的流中(忽略 top, bottom, left, right 或者 z-index 声 明)。

##### 6.inherit:

规定应该从父元素继承 position 属性的值。

#### 16.浮动清除

##### 方法一:使用带 clear 属性的空元素

 在浮动元素后使用一个空元素如<div class="clear"></div>，并在 CSS 中赋 予.clear{clear:both;}属性即可清理浮动。亦可使用<br class="clear" />或<hr class="clear" /> 来进行清理。

#####  方法二:使用 CSS 的 overflow 属性

 给浮动元素的容器添加 overflow:hidden;或 overflow:auto;可以清除浮动，另外在 IE6 中还 需要触发 hasLayout ，例如为父元素设置容器宽高或设置 zoom:1。
 在添加 overflow 属性后，浮动元素又回到了容器层，把容器高度撑起，达到了清理浮动 的效果。

#####  方法三:

给浮动的元素的容器添加浮动 给浮动元素的容器也添加上浮动属性即可清除内部浮动，但是这样会使其整体浮动，影 响布局，不推荐使用。

#####  方法四:

使用邻接元素处理
 什么都不做，给浮动元素后面的元素添加 clear 属性。

#####  方法五:使用 CSS 的:after 伪元素

 结合:after 伪元素(注意这不是伪类，而是伪元素，代表一个元素之后最近的元素)和 IEhack ，可以完美兼容当前主流的各大浏览器，这里的 IEhack 指的是触发 hasLayout。 给浮动元素的容器添加一个 clearfix 的 class，然后给这个 class 添加一个:after 伪元素实 现元素末尾添加一个看不见的块元素(Block element)清理浮动。
 参考 https://www.cnblogs.com/ForEvErNoME/p/3383539.html

#### 17.CSS 选择器有哪些，优先级呢

id 选择器，class 选择器，标签选择器，伪元素选择器，伪类选择器等 同一元素引用了多个样式时，排在后面的样式属性的优先级高; 样式选择器的类型不同时，优先级顺序为:id 选择器 > class 选择器 > 标签选择器; 标签之间存在层级包含关系时，后代元素会继承祖先元素的样式。如果后代元素定义了 与祖先元素相同的样式，则祖先元素的相同的样式属性会被覆盖。继承的样式的优先级 比较低，至少比标签选择器的优先级低;
 带有!important 标记的样式属性的优先级最高; 样式表的来源不同时，优先级顺序为:内联样式> 内部样式 > 外部样式 > 浏览器用户 自定义样式 > 浏览器默认样式

#### 18.css 动画如何实现

创建动画序列，需要使用 animation 属性或其子属性，该属性允许配置动画时间、时长 以及其他动画细节，但该属性不能配置动画的实际表现，动画的实际表现是由 @keyframes 规则实现，具体情况参见使用 keyframes 定义动画序列小节部分。 transition 也可实现动画。transition 强调过渡，是元素的一个或多个属性发生变化时产生 的过渡效果，同一个元素通过两个不同的途径获取样式，而第二个途径当某种改变发生 (例如 hover)时才能获取样式，这样就会产生过渡动画。

#### 19.如何实现图片在某个容器中居中的?

父元素固定宽高，利用定位及设置子元素 margin 值为自身的一半。 父元素固定宽高，子元素设置 position: absolute，margin:auto 平均分配 margin css3 属性 transform。子元素设置 position: absolute; left: 50%; top: 50%;transform: translate(-50%,-50%);即可。
 将父元素设置成 display: table, 子元素设置为单元格 display: table-cell。 弹性布局 display: flex。设置 align-items: center; justify-content: center

#### 20.三栏布局的实现方式，尽可能多写，浮动布局时，三个 div 的生成顺序有没有影响

三列布局又分为两种，两列定宽一列自适应，以及两侧定宽中间自适应

两列定宽一列自适应:
 1、使用 float+margin:
 给 div 设置 float:left，left 的 div 添加属性 margin-right:left 和 center 的间隔 px,right 的 div 添加属性 margin-left:left 和 center 的宽度之和加上间隔
 2、使用 float+overflow:
 给 div 设置 float:left，再给 right 的 div 设置 overflow:hidden。这样子两个盒子浮动，另 一个盒子触发 bfc 达到自适应
 3、使用 position:
 父级 div 设置 position:relative，三个子级 div 设置 position:absolute，这个要计算好盒 子的宽度和间隔去设置位置，兼容性比较好，
 4、使用 table 实现:
 父级 div 设置 display:table，设置 border-spacing:10px//设置间距，取值随意,子级 div 设置 display:table-cell，这种方法兼容性好，适用于高度宽度未知的情况，但是 margin 失效，设计间隔比较麻烦，
 5、flex 实现:
 parent 的 div 设置 display:flex;left 和 center 的 div 设置 margin-right;然后 right 的 div 设置 flex:1;这样子 right 自适应，但是 flex 的兼容性不好
 6、grid 实现:
 parent 的 div 设置 display:grid，设置 grid-template-columns 属性，固定第一列第二列宽 度，第三列 auto，
 对于两侧定宽中间自适应的布局，对于这种布局需要把 center 放在前面，可以采用双飞 翼布局:圣杯布局，来实现，也可以使用上述方法中的 grid，table，flex，position 实现

#### 21.calc 属性

Calc 用户动态计算长度值，任何长度值都可以使用 calc()函数计算，需要注意的是，运 算符前后都需要保留一个空格，例如:width: calc(100% - 10px);

#### 22.z-index 的定位方法

z-index 属性设置元素的堆叠顺序，拥有更好堆叠顺序的元素会处于较低顺序元素之前， z-index 可以为负，且 z-index 只能在定位元素上奏效，该属性设置一个定位元素沿 z 轴的位置，如果为正数，离用户越近，为负数，离用户越远，它的属性值有 auto，默认， 堆叠顺序与父元素相等，number，inherit，从父元素继承 z-index 属性的值

#### 23.line-height 和 height 的区别

line-height 一般是指布局里面一段文字上下行之间的高度，是针对字体来设置的，height 一般是指容器的整体高度。

#### 24.inline-block、inline 和 block 的区别;为什么 img 是 inline 还可以设置宽高

block 元素会独占一行，多个 block 元素会各自新起一行。默认情况下，block 元素宽度 自动填满其父元素宽度。
 block 元素可以设置 width,height 属性。块级元素即使设置了宽度,仍然是独占一行。 block 元素可以设置 margin 和 padding 属性。

inline 元素不会独占一行，多个相邻的行内元素会排列在同一行里，直到一行排列不下， 才会新换一行，其宽度随元素的内容而变化。
 inline 元素设置 width,height 属性无效。
 inline 元素的 margin 和 padding 属性，水平方向的 padding-left, padding-right, margin-left, margin-right 都产生边距效果;但竖直方向的 padding-top, padding-bottom, margin-top, margin-bottom 不会产生边距效果。

inline-block:简单来说就是将对象呈现为 inline 对象，但是对象的内容作为 block 对象 呈现。之后的内联对象会被排列在同一行内。比如我们可以给一个 link(a 元素) inline-block 属性值，使其既具有 block 的宽度高度特性又具有 inline 的同行特性。

#### 25.overflow 的原理

要讲清楚这个解决方案的原理，首先需要了解块格式化上下文，A block formatting context is a part of a visual CSS rendering of a Web page. It is the region in which the layout of block boxes occurs and in which floats interact with each other.翻译过来就是块格式化上下文是 CSS 可视化渲染的一部分，它是一块区域，规定了内部块盒 的渲染方式，以及浮动相 互之间的影响关系
 当元素设置了 overflow 样式且值部位 visible 时，该元素就构建了一个 BFC，BFC 在计算 高度时，内部浮动元素的高度也要计算在内，也就是说技术 BFC 区域内只有一个浮动 元素，BFC 的高度也不会发生塌缩，所以达到了清除浮动的目的。

#### 26.使元素消失的方法有哪些

1.opacity:0，该元素隐藏起来了，但不会改变页面布局，并且，如果该元素已经绑定 一些事件，如 click 事件，那么点击该区域，也能触发点击事件的

2.visibility:hidden，该元素隐藏起来了，但不会改变页面布局，但是不会触发该元素已 经绑定的事件

3。display:none，把元素隐藏起来，并且会改变页面布局，可以理解成在页面中把该元 素删除掉。

#### 27.css布局

六种布局方式总结:圣杯布局、双飞翼布局、Flex 布局、绝对定位布局、表格布局、网 格布局。
 圣杯布局是指布局从上到下分为 header、container、footer，然后 container 部分定为三栏 布局。这种布局方式同样分为 header、container、footer。圣杯布局的缺陷在于 center 是 在 container 的 padding 中的，因此宽度小的时候会出现混乱。
 双飞翼布局给 center 部分包裹了一个 main 通过设置 margin 主动地把页面撑开。
 Flex 布局是由 CSS3 提供的一种方便的布局方式。
 绝对定位布局是给 container 设置 position: relative 和 overflow: hidden，因为绝对定位的元 素的参照物为第一个 postion 不为 static 的祖先元素。 left 向左浮动，right 向右浮动。 center 使用绝对定位，通过设置 left 和 right 并把两边撑开。 center 设置 top: 0 和 bottom: 0 使其高度撑开。
 表格布局的好处是能使三栏的高度统一。 网格布局可能是最强大的布局方式了，使用起来极其方便，但目前而言，兼容性并不好。 网格布局，可以将页面分割成多个区域，或者用来定义内部元素的大小，位置，图层关 系。

参考：https://juejin.im/post/599970f4518825243a78b9d5#heading-22

#### 28.移动布局方案

##### 一、rem 单位如何转换为像素值

 1.当使用 rem 单位的时候，页面转换为像素大小取决于叶根元素的字体大小，即 HTML 元素的字体大小。根元素字体大小乘 rem 的值。例如，根元素的字体大小为 16px，那么 10rem 就等同于 10*16=160px。

#####  二、em 是如何转换成 px 的

 当使用 em 单位的时候，像素值是将 em 值乘以使用 em 单位的元素的字体大小。例如一 个 div 的字体为 18px，设置它的宽高为 10em，那么此时宽高就是 18px*10em=180px。 .test{

width: 10em;
 height: 10em; background-color: #ff7d42; font-size: 18px;

}

一定要记住的是，em 是根据使用它的元素的 font-size 的大小来变化的，而不是根据父 元素字体大小。有些元素大小是父元素的多少倍那是因为继承了父元素中 font-size 的设 定，所以才起到的作用。
 2.em 单位的继承效果。

使用 em 单位存在继承的时候，每个元素将自动继承其父元素的字体大小，继承的效果 只能被明确的字体单位覆盖，比如 px 和 vw。只要父级元素上面一直有 fontsize 为 em 单 位，则会一直继承，但假如自己设置了 font-size 的单位为 px 的时候，则会直接使用自 己的 px 单位的值。

##### 三、根 html 的元素将会继承浏览器中设置的字体大小

除非显式的设置固定值去覆盖。所以 html 元素的字体大小虽然是直接确定 rem 的值， 但这个字体大小首先是来源于浏览器的设置。(所以一定要设置 html 的值的大小，因 为有可能用户的浏览器字体大小是不一致的。)
 四、当 em 单位设置在 html 元素上时

它将转换为 em 值乘以浏览器字体大小的设置。 例如:
 html{

font-size: 1.5em; }

可以看到，因为浏览器默认字体大小为 16px，所以当设置 HTML 的 fontsize 的值为 1.5em 的售后，其对应的 px 的值为 16*1.5=24px
 所以此时，再设置其他元素的 rem 的值的时候，其对应的像素值为 n*24px。 例如，test 的 rem 的值为 10，

.test{
 width: 10rem;

height: 10rem;

background-color: #ff7d42; }

![](/Users/liangjiahao/Pictures/截图图库/截屏2022-03-15 22.53.43.png)

可以看到 test 的 font-size 继承了 html 的值 24px，而此时宽高为 24*10=240px 总结

1. rem 单位翻译为像素值的时候是由 html 元素的字体大小决定的。此字体大小会 被浏览器中字体大小的设置影响，除非显式的在 html 为 font-size 重写一个单位。

2. em 单位转换为像素值的时候，取决于使用它们的元素的 font-size 的大小，但是有 因为有继承关系，所以比较复杂。
    优缺点
    em 可以让我们的页面更灵活，更健壮，比起到处写死的 px 值，em 似乎更有张力，改 动父元素的字体大小，子元素会等比例变化，这一变化似乎预示了无限可能,

em 做弹性布局的缺点还在于牵一发而动全身，一旦某个节点的字体大小发生变化，那 么其后代元素都得重新计算

#### 29.flex 布局及优缺点(p128)

参考回答:https://juejin.im/post/599970f4518825243a78b9d5#heading-22

#### 30.Rem 布局及其优缺点(p129)

#### 31.移动端适配 1px 的问题

参考：https://blog.csdn.net/weixin_43675871/article/details/84023447

首先，我们了解 devicePixelRatio(DPR)这个东西

在 window 对象中有一个 devicePixelRatio 属性，他可以反应 css 中的像素与设备 的像素比。然而 1px 在不同的移动设备上都等于这个移动设备的 1px，这是因为 不同的移动设备有不同的像素密度。有关这个属性，它的官方的定义为:设备物 理像素和设备独立像素的比例，也就是 devicePixelRatio = 物理像素 / 独立像素 1px 变粗的原因:viewport 的设置和屏幕物理分辨率是按比例而不是相同的. 移动 端 window 对象有个 devicePixelRatio 属性,它表示设备物理像素和 css 像素的比例, 在retina屏的iphone手机上, 这个值为2或3,css里写的1px长度映射到物理像素 上就有 2px 或 3px 那么长

1.用小数来写 px 值 (不推荐)
 IOS8 下已经支持带小数的 px 值, media query 对应 devicePixelRatio 有个查询值 -webkit-min-device-pixel-ratio, css 可以写成这样 通过-webkit-min-device-pixel-ratio 设置。
 .border { border: 1px solid #999 }
 @media screen and (-webkit-min-device-pixel-ratio: 2) {

.border { border: 0.5px solid #999 } }

@media screen and (-webkit-min-device-pixel-ratio: 3) { .border { border: 0.333333px solid #999 }

}

如果使用 less/sass 的话只是加了 1 句 mixin
 缺点: 安卓与低版本 IOS 不适用, 这个或许是未来的标准写法, 现在不做指望 2、flexible.js
 这是淘宝移动端采取的方案, github 的地址:https://github.com/amfe/lib-flexible. 前面已经 说过 1px 变粗的原因就在于一刀切的设置 viewport 宽度, 如果能把 viewport 宽度设置 为实际的设备物理宽度, css 里的 1px 不就等于实际 1px 长了么. flexible.js 就是这样 干的.
 <meta name=”viewport”>里面的 scale 值指的是对 ideal viewport 的缩放, flexible.js 检 测到 IOS 机型, 会算出 scale = 1/devicePixelRatio, 然后设置 viewport
 3、伪类+transform 实现
 对于解决 1px 边框问题，我个人觉得最完美的解决办法还是伪类+transform 比较好。 原理:是把原先元素的 border 去掉，然后利用 :before 或者 :after 重做 border ，并 transform 的 scale 缩小一半，原先的元素相对定位，新做的 border 绝对定位。
 media query 通过媒体查询，可以通过给不同分辨率的设备编写不同的样式来实现响应式的布局，比 如我们为不同分辨率的屏幕，设置不同的背景图片。比如给小屏幕手机设置@2x 图，为 大屏幕手机设置@3x 图，通过媒体查询就能很方便的实现。 但是媒体查询的缺点也很明显，如果在浏览器大小改变时，需要改变的样式太多，那么 多套样式代码会很繁琐。
 @media screen and (min-width: 320px) {

html {
 font-size: 50px;

} }

@media
 方便应用广泛 适用于 pc 端 手机页面，通常做自适应布局时 我们比较常用。 缺点:相对于代码要重复很多，得知道设备的宽度，手机的分辨率很多所以麻烦了点， 不过性能方面肯定最高; 可能存在闪屏的问题
 @media 处理手机和 pc 端界面兼容的问题，在 IE 上的访问出现问题，百度方法，找找 两种，一种是 respond.js，另一种是 css3-mediaquerieshttp://blog.csdn.net/small_tu/article/details/47317453

#### 32.移动端性能优化相关经验

参考：https://blog.csdn.net/tangxiujiang/article/details/79791545