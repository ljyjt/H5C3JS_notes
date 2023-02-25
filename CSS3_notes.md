# 1.CSS基本概念

<p style="color:rgb(241, 157, 56);font-size:20px">层叠样式表（Cascading Style Sheets）</p>

[CSS样式表/级联样式表]

- **标记语言**

=> <u>美化HTML</u>，让HTML更漂亮，让页面布局更简单



# 2.CSS字体属性

## ①字体系列 font-family

定义文本的字体

```css
div {
  font-family: Arial,"Microsoft Yahei","微软雅黑"
}

【注：多种字体逗号分割
   中间有空格，用引号包起来
   同时写多种字体，以首字体显示，无则自动显示下一类字体】
```

## ②字体大小 font-size

- 谷歌默认文字大小为**16px**
- 单位： px
- 可以给body指定整个页面的文字大小，标题标签需单独指定

## ③字体粗细 font-weight

```text
normal            默认（400）
bold              粗体（700）
100-900          【数字后面不跟单位】
```

## ④文字样式 font-style

```text
normal            默认值，标准字体样式
italic            斜体
```

## ⑤字体复合属性

顺序 ： **SWSF**        

```css
body {
  font: font-style font-weight font-size/line-height font-family;
}
```

- 必须保留 <u>font-size</u>、<u>font-family</u>



# 3.CSS文本属性

## ①文本颜色 Color

```text
预定义的颜色值         pink/blue
十六进制              #FFF
rgb代码              rgb(255,0,0)
```

## ②对齐文本 text-align 

设置文本的水平对齐方式

```text
left                 左对齐【默认值】
center               居中
right                右对齐
```

## ③装饰文本 text-decoration

```text
none               没有装饰线【默认值】
underline          下划线（链接a自带下划线）
overline           上划线
line-through       删除线
```

## ④文本缩紧 text-indent

指定文本第一行的缩进        px / em

## ⑤行间距 line-height

控制文字行与行之间的距离



# 4.CSS引入方式

## ①内部样式表

嵌入式引入 —— 使用`<style></style>`标签，在`<head><head/>`标签内书写

没有实现结构与样式的分离

## ②行内样式表

行内式引入 —— 在元素标签内使用**style属性**设置

适合修改简单样式

## ③外部样式表

外链式 / 链接式引入

实现结构与样式的完全分离

- 新建一个.css的样式文件

- 在HTML页面中，使用`<link>`标签引入这个css文件

- ```text
  ref            stylesheet，链接的文档是一个样式表文件
  href           链接外部样式表文件的URL
  ```



# 5.CSS基础选择器

由单个选择器组成

## ① 标签选择器 

- 以**HTML标签名称**作为选择器 => **某一类全部标签**

## ② 类选择器 

<p style="color:rgb(205, 87, 73);font-size:18px">选择1个或多个标签</p>

- 用 **class** 定义       

-  "**.**"进行标识，后面紧跟类名

- ```text
  样式点定义
  结构类调用
  一个或多个
  开发最常用
  ```

## ③ id选择器

<p style="color:rgb(205, 87, 73);font-size:18px">一次只能选择1个标签</p>

- 用 **#** 定义

- ```text
  样式#定义
  结构id调用
  只能调一次
  别人切勿用
  ```

## ④ 通配符选择器

- 用 ***** 定义
- 选取页面中的所有元素



# 6.CSS复合选择器

两个或多个选择器，通过不同方式组合而成

## ①🌟后代选择器（空格）

```text
元素1 元素2 { 样式声明 }
```

选择元素1里面所有的元素2（后代元素，可以是儿子或孙子）

## ②🌟子选择器（>）

```text
元素1 > 元素2 { 样式声明 }
```

选择元素1中所有的直接后代（子元素【亲儿子】）元素2

## ③🌟并集选择器（,）

```text
元素1,元素2 { 样式声明 }
```

选择多组标签，同时为他们定义相同样式

## ④伪类选择器

用于向某些选择器**添加特殊效果**

```text
链接：

a:link           选择所有未被访问的链接
a:visited        选择所有已被访问的链接
a:hover          选择鼠标指针位于其上的链接
a:active         选择活动链接（鼠标按下未弹起的链接）

【顺序 ： LVHA】
```

```text
表单：

input:focus {
	background-color: yellow;
}
```



# 7.CSS的三大特性

## ①层叠性

- 给相同选择器设置相同样式，一个样式就会**覆盖（层叠）**另一个冲突的样式
- **样式冲突** —— 就近原则

## ②继承性

- 子标签继承父标签的某些样式（与文字相关的样式：text- / font- / line- / color）

## ③优先级

```text
继承 或 *                         0,0,0,0
元素选择器（如div）                 0,0,0,1
类选择器 / 伪类选择器（如.class）    0,0,1,0
id选择器（如#id）                  0,1,0,0
行内样式                           1,0,0,0
！important                       ∞无穷大
```



# 8.CSS的元素显示模式

## ①块元素

```text
<h1> - <h6>
<p>
<div>
<form> 
<tabel> <tr> <th> 
<ul>
<ol>
<li>
<dl> <dt> <dd>
<hr />
<nav>
<address>
<blockquote>
```

- 特点
  - 独占一样，宽度默认容器100%
  - 高度、宽度、内外边距都可以控制
  - 是一个容器及盒子

- 注意
  - 文字类的元素内不能使用块级元素（`<p></p>` `<h1>-<h6>`）

## ②行内元素（内联元素）

```text
<a>
<strong> <b> <em> <i> <del> <s> <ins> <u>
<br />
<span>
<label>
<canvas>
```

- 特点
  - 一行可以显示多个
  - **高、宽设置无效**
  - 默认宽度为本身内容的宽度
  - 只能收纳文本或其他行内元素

- 注意
  - 链接内不能再放链接

## ③行内块元素

```text
<img />
<input />
<td>
```

- 特点
  - （行内元素特点）一行可以显示多个
  - （行内元素特点）默认宽度为本身内容宽度
  - （块级元素特点）宽度、高度、外边距、内边距都可以控制

## ④元素显示模式转换

一个模式的元素需要另外一种模式的特性

```css
display: block;          转为块元素（ 设置宽高 ）
display: inline;         转为行内元素（ 一行放多个块 ）
display: inline-block;   转为行内块元素（ 一行放多个且能设置宽高）
```



# 🌰 单行文字垂直居中

​       —— height = line-height



# 9.CSS的背景

## ①背景颜色 background-color

一般元素背景默认值为transparent

## ②背景图片 background-image

背景图片 会**覆盖 背景颜色**

```text
background-image: url(“xxxx.jpg”);

none              无背景图【默认值】
url(路径)          指定背景图的路径
```

## ③背景平铺 background-repeat

```text
repeat            背景图在纵向和横向上平铺【默认值】
no-rapeat         不平铺
repeat-x          在横向上平铺
repeat-y          在纵向上平铺
```

## ④背景图片位置 background-position

```text
background-position: x y;

length            百分数 / 数值
position          方位名词 top / center / bottom / left / center / right 
```

## ⑤背景图像固定 background-attachment

设置背景图片是否固定或随页面的其余部分滚动

```text
scroll            背景图像是否随对象内容滚动【默认值】
fixed             背景图像固定
```

## ⑥背景复合写法

没有特定的书写顺序

```text
background: transparent url(image.jpg) repeat-y fixed top;
```

## ⑦背景颜色半透明

```text
background: rgba(0,0,0,0.3);
```

- 最后一个参数为alpha透明度，0-1
- 盒子背景半透明，盒子内容不受影响



# 10.盒子模型

## ①边框 border

```text
border-width               边框粗细
border-style               边框样式  solid  dashed(虚线)  dotted(点线)
border-color               黑色【默认】
```

简写：

```css
border: 1px solid red;  没有顺序
```

边框分开写法：

```css
border-top: 1px solid red;   只设置上边框
```

- 表格细线边框 border-collapse
  - 控制相邻单元格的边框 —— 相邻边框合并在一起

<p style="color:rgb(223, 96, 84);font-size:25px">注意 ⚠️ ：边框会影响盒子的实际大小</p>

## ②内边距 padding

设置边框与内容间的距离（默认挨在一起）

```text
padding-left            左内边距
padding-right           右内边距
padding-top             上内边距
padding-bottom          下内边距
```

<p style="color:rgb(223, 96, 84);font-size:25px">注意 ⚠️ ：如果盒子没有指定width/height，则padding不会撑开盒子大小</p>

## ③外边距 margin

设置盒子与盒子间的距离

```text
margin-left             左外边距
margin-right            右外边距
margin-top              上外边距
margin-bottom           下外边距
```

- 外边距合并

  - 【相邻块元素】

    上面元素的下边距与下面元素的上边距，会取而这种较大的值进行合并

    ​	——  尽量只给一个盒子添加margin

  - 【嵌套块元素】

    父子元素均有上外边距，会塌陷使用较大的值



### 🌰 块元素水平居中

```text
盒子指定宽度

左右外边距设置为auto

         —— margin: 0 auto;
```



## ④圆角边框 border-radius

```css
border-radius: length圆半径;

参数为 数值 或 百分比
```

- 圆形 —— `radius = height 或 width;`
- 圆角矩形 —— `radius = height/2;`

## ⑤盒子阴影 border-shadow

阴影不占用空间，不影响其他盒子排列

```text
h-shadow             x轴 水平阴影【必需】
v-shadow             y轴 垂直阴影【必需】
blur                 模糊距离（影子虚实）
spread               阴影的尺寸
color                阴影的颜色
inset                内部阴影【默认外阴影（outset）】
```

```css
box-shadow: h-shadow v-shadow blur spread color inset;
```

## ⑥文字阴影 text-shadow

```text
h-shadow             x轴 水平阴影【必需】
v-shadow             y轴 垂直阴影【必需】
blur                 模糊距离（影子虚实）
color                阴影的颜色x
```

```css
text-shadow: h-shadow v-shadow blur color;
```



# 11.页面布局

## ①标准流

标签按规定好的默认方式排列

- 块元素 ：独占一行，从上向下排列
- 行内元素 ：从左向右排列，遇到父元素边缘自动换行

## ②浮动 float

```css
div {
  float： 属性值;
}
```

```text
none              不浮动【默认值】
left              左浮动
right             右浮动
```

- 特点
  - **脱离标准流**，不再保留原先的位置
  - 浮动的元素会<u>一行内显示</u>并元素<u>顶部对齐</u>
  - 具备**行内块特性**
    - 块级盒子浮动后，大小由内容决定
    - 浮动的盒子中间没有空隙

- 浮动元素经常和标准流父级搭配使用
  - 网页布局第一准则：**标准流父元素排列上下位置，内部子元素采取浮动排列左右位置**
  - 网页布局第二准则：先设置盒子大小，后设置盒子位置

- 注意点
  - 浮动和标准流的父盒子搭配
  - 一个元素浮动了，理论上其余兄弟元素也要浮动

- 清除浮动

  ​           —— 标准流的父盒子不方便给高度，但子盒子浮动后不占位置，最后父盒子高度为0，影响下面的标准流

  - 1⃣️ 额外标签法

    - 浮动元素末尾添加一个空标签

      ```css
      div { clear: both; }
      ```

  - 2⃣️ 父级添加overflow

    - 属性包括 hidden / auto / scroll

      ```css
      父级元素 { overflow: hidden; }
      ```

    - 无法显示溢出部分

  - 3⃣️ :after伪元素法

  - 4⃣️ 双伪元素法

## ③定位 position

- 定位模式

  ```text
  static               静态定位【默认值】
  relative             相对定位
  absolute             绝对定位
  fixed                固定定位
  ```

- 边偏移

  ```text
  top                  顶端偏移量
  bottom               底部偏移量
  left                 左侧偏移量
  right                右侧偏移量
  ```

- 定位叠放次序 z-index
  - 只有定位的盒子有z-index属性
  - 数值后不加单位
  - 数值越大，盒子越靠上
  - 若数值相同，按照书写顺序，后来居上

### (1)静态定位 static

​				无定位【默认值】

### (2)🌟相对定位 relative

 				——相对于原来的位置移动

- **不脱标**
- 给绝对定位当爹

### (3)🌟绝对定位 absolute

​				——相对于祖先元素移动

- **脱标**

- 若没有祖先元素，以浏览器为准定位

  <p style="color:rgb(223, 96, 84);font-size:25px">子绝父相</p>

### (4)🌟固定定位 fixed

​				——固定在浏览器可视区的位置

- 脱标
- 以**浏览器的可视窗口**为参照点移动元素（不随滚动条滚动）



### 🌰 绝对定位的盒子居中

```text
left: 50%;                  让盒子的左侧移动到父元素中心位置
margin-left: -100px;        让盒子向左移动自身宽度的一半
```

<p style="color:rgb(223, 96, 84);font-size:25px">绝对（固定）定位元素 会完全压住盒子<br/>浮动元素 会压住标准流盒子但不会压住盒子里的文字</p>



# 12.CSS的属性书写顺序

- 布局定位属性：display、position、float、clear、visibility、overflow
- 自身属性：width、height、margin、padding、border、background
- 文本属性：color、font、text-decoration、text-align、vertical-align、white-space、break-word
- 其他属性：content、cursor、border-radius、box-shadow、text-shadow



# 13.元素的显示与隐藏

## ①display属性

 	 	——设置一个元素如何显示

```text
display: none;          隐藏对象
display: block;         显示元素
```

- 隐藏元素后，**不再占有原来的位置**

## ②visibility可见性

​			——指定一个元素可见还是隐藏

```text
visibility: visible;    元素可视
visibility: hidden;     元素隐藏
```

- 隐藏元素后，继续**占有原来的位置**

## ③overflow溢出

​			——如果内容溢出一个元素的框时，会发生什么

```text
visible            不剪切内容也不添加滚动条
hidden             不显示超过对象尺寸的内容，超出的部分隐藏掉
scroll             不管是否超出内容，总是显示滚动条
auto               超出自动显示滚动条，不超出不现实滚动条
```



### 🌰 精灵图

```text
为有效减少服务器接收和发送请求的次数，提高页面加载速度

将网页中的小背景图整合到一张大图中，这样服务器只需一次请求即可

借助背景图片位置移动来实现【向上向左 => 负值； 向下向右 => 正值；】
```



# 14.CSS用户界面样式

- 鼠标样式 cursor

  ```text
  default            【默认】
  pointer             小手
  move                移动（四方箭头）
  text                文本
  not-allowed         禁止 
  ```

- 表单轮廓线 outline

  添加 `input {outline: 0/none;}` 去掉默认蓝色边框

- 文本域防止拖拽 resize

  文本域右下角默认可以拖拽，添加 `textarea {resize: none;}` 就不可以拖拽



# 15.vertical-align 属性

设置元素**垂直对齐的方式**，只针对<u>行内元素</u>和<u>行内块元素</u>有效

```text
baseline               基线【默认值】
top                    顶线
middle                 中部
bottom                 底线
```



### 🌰 解决图片底部默认空白缝隙

（bug：**行内块元素**会和文字的**基线对齐**）

```text
▪︎ 🌟vertical-align: middle | top | bottom
▪︎ 将图片转换为块级元素
```



# 🌰 溢出的文字省略号显示

- 单行文本溢出显示省略号

  ```text
  1.强制一行内显示文本
  	white-space: no-wrap;    (默认 normal 自动换行)
  2.超出的部分隐藏
  	overflow: hidden;
  3.文字用省略号替代超出的部分
  	text-overflow: ellipsis;
  ```



# 16.CSS3的新特性

新增选择器、盒子模型、其他特性

## ①新增选择器

### (1)属性选择器

​				【**权重10**】

​				——根据元素特定属性来选择元素（不用借助于类或id选择器）

```text
E[att]                 具有att属性的E元素
E[att="val"]           具有att属性且属性值等于val的E元素
E[att^="val"]          具有att属性且属性值以val开头的E元素
E[att$="val"]          具有att属性且属性值以val结尾的E元素
E[att*="val"]          具有att属性且属性值中含有val的E元素
```

### (2)结构伪类选择器

​				【**权重10**】				

​				——根据父级选择器的子元素

```text
E:first-child          匹配父元素中的第一个子元素E
E:last-child           匹配父元素中的最后一个子元素E
E:nth-child(n)         匹配父元素中的第n个子元素E
```

```text
E:first-of-type        指定类型E的第一个子元素
E:last-of-type         指定类型E的最后一个子元素
E:nth-of-type(n)       指定类型E的第n个子元素
```

- nth-child(n) ｜ nth-of type(n)

  - n**从0开始计算**
  - n可以是**数字**，也可以是**公式**

  - n可以是**关键字**（偶even、奇odd）

- 区别

  - nth-child对父元素里所有孩子排序选择，**先找到第n个孩子**，再看是否和E匹配

  - nth-of-type对父元素里指定子元素排序选择，**先匹配E**，再根据E找第n个孩子

### (3)🌟伪元素选择器

​				【**权重1**】

​				——利用CSS创建新标签元素，而不需要HTML标签

```text
::before               在元素内部的前面插入内容
::after                在元素内部的后面插入内容
```

- 创建的元素属于**行内元素**
- before与after**必须有content属性**

## ②CSS3盒子模型

- box-sizing 指定盒模型
  - **content-box**
    - 盒子大小为 width+padding+border（以前默认的）
  - **border-box**
    - 盒子大小为 width
    - padding与border不会撑开盒子（不超过width）

## ③CSS3其他特性

### (1)滤镜 filter

**模糊**或**颜色偏移**等图形效果应用于元素

```css
filter: 函数();

filter: blur(5px);  模糊处理，数值越大越模糊
```

### (2)calc函数

在声明CSS属性值时**执行一些计算**

```css
width: calc(100% - 80px);    (可以用+、-、*、/进行计算，前后加空格)
```

### (3)🌟过渡 transition

从一个状态渐渐过渡到另一个状态（常与:hover搭配使用）

谁做过渡给谁加：

```css
transition: 要过渡的属性 花费时间 运动曲线 何时开始;
```

- **属性**：宽、高、背景颜色等；若所有属性都变化过渡 => all
- **花费时间**：秒
- <u>运动曲线</u>：ease【默认】、linear（线性）、ease-in（缓进）、ease-out（缓出）、ease-in-out（缓进出）

- <u>何时开始</u>：秒      设置延迟触发时间，默认0s

### (4)2D转换 transform

#### 1⃣️ 移动 translate

改变元素在页面中的位置，类似于定位

```css
transform: translate(x,y);

transform: translateX(n);
transform: translateY(n);
```

- 不会影响到其他元素的位置
- 百分比单位 相较于自身元素的translate(50%,50%);
- 对行内标签没有效果

#### 2⃣️ 旋转 rotate

让元素在平面内顺时针旋转或逆时针旋转

```css
transform: rotate(度数);
```

- 度数单位：deg
- 顺时针（角度为正），逆时针（角度为负）
- 默认旋转中心：元素中心点

#### 3⃣️ 缩放 scale

```css
transform: scale(x,y);
```

- transform: scale(2,2);	宽、高都放大了2倍
- transform: scale(2);       只写一个参数，第二个参数与第一个参数一样
- 设置转换中心点缩放，不影响其他盒子

#### 4⃣️ 转换中心点 transform-origin

设置元素转换的中心点

```css
transform-origin: x y;
```

- 百分比、数值、方位词
- 默认（50% 50%）

#### 5⃣️ 综合写法

- 同时使用多种转换，格式为：transform: **translate() rotate() scale()**
- 写的<u>顺序会影响转换效果</u>
- **当同时有位移及其他属性时，<u>将位移放在最前</u>**

### (5)动画 animation

- 定义动画

  ```css
  @keyframes 动画名称 {
    0% | from {}
    100% | to {}
  }
  
  div {
    /*调用动画*/
    animation-name: 动画名称;
    /*持续时间*/
    animation-duration: 持续时间;
  }
  ```

- 动画常用属性

  ```text
  @keyframes                      规定动画
  animation-name                  动画名称     【必需】
  animation-duration              动画持续时间  【必需】
  animation-timing-function       速度曲线 ease
  animation-delay                 何时开始 0
  animation-iteration-count       被播放次数 normal （infinite）
  
  animation-play-state            是否正在运行或暂停 running （paused）
  														   【搭配hover】					
  																
  animation-direction             下一周期逆向播放 normal （alternate）
  															 【动画走回来，而不是跳回来 => alternate】
  															 
  animation-fill-mode             动画结束后状态 backwards （forwards）
  															 【动画结束后，停在结束位置 => forwards】
  ```

### (6)3D转换

- x轴          右正、左负
- y轴          下正、上负
- z轴           外正、内负

#### 1⃣️ 3D移动 translate3d

```css
transform: translate3d(x,y,z);

transform: translateX(100px);
transform: translateY(100px);
transform: translateZ(100px);
```

#### 2⃣️ 3D旋转 rotate3d

```css
transform: rotate3d(0,0,1,45deg); /*向z轴旋转45度*/

transform: rotateX(45deg);
transform: rotateY(45deg);
transform: rotateZ(45deg);
```

#### 3⃣️ 透视 perspective

写到**被观察元素的父盒子**上

- （视距）—— 人眼睛到屏幕的距离
  - 越近成像越大，越远成像越小

#### 4⃣️ 3D呈现 transform-style

- **写给<u>父级</u>，影响子盒子**
- `transform-style: flat` 子元素**不开启**3d立体空间
- `transform-style: preserve-3d` 子元素**开启**3d立体空间

### (7)浏览器私有前缀

```text
-moz-             firefox浏览器私有属性
-ms-              ie浏览器私有属性
-webkit-          safari、chrome浏览器私有属性
-o-               Opera浏览器私有属性
```

