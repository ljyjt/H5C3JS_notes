# 一、API与Web API

- API（Application Programming Interface应用程序编程接口）

  ​	—— 预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件得以访问一组程例的能力，而又无需访问源码，或理解内部工作机制的细节。

  

- Web API

  ​    —— 浏览器提供的一套操作**浏览器功能**和**页面元素**的**API**（BOM和DOM）

  - 针对浏览器提供的接口，主要是对于浏览器做交互效果

# 二、DOM

（Document Object Model）
—— W3C组织推荐的处理可扩展标记语言的标准**编程接口**，可以改变<u>网页的内容、结构和样式</u>

- DOM树
  - 文档 document —— 一个页面就是一个文档
  - 元素 element     —— 页面中的所有标签
  - 节点 node           —— 网页中的所有内容

## 1.获取元素

### (1)ID获取

​		—— 获取带有ID的**元素对象**

`document.getElementById('id')`    若没找到则返回null

### (2)标签名获取

​		—— 获取带有指定标签名的**元素对象集合**

`document.getElementByTagName('标签名')`  

- 若页面中只有一个该类型元素，返回的是**伪数组的形式**
- 若页面中没有这种元素，返回**空伪数组**

### (3)H5新方法

#### ① 类名

​		—— 根据类名返回**元素对象集合**

`document.getElementByClassName('类名')`

#### ② 选择器

​		 ['#id', '.class', 'div']

- `document.querySelector('选择器')`  —— 根据指定选择器返回**第一个元素对象**

- `document.querySelectorAll('选择器')` —— 根据指定选择器返回**所有元素集合**

#### ④ 获取特殊元素(body, html)

- 获取body元素对象  ——  `document.body`
- 获取html元素对象  ——  `document.documentElement`

## 2.事件基础

- 事件三要素 
  - 事件源 —— 事件被触发的对象
  - 事件类型 —— 如何触发，什么事件
  - 事件处理程序 —— 通过一个函数赋值的方式完成

- 执行事件的步骤
  - 1⃣️ 获取事件源
  - 2⃣️ 注册事件（绑定事件）
  - 3⃣️ 添加事件处理程序（采取函数赋值方式）

## 3.操作元素

利用DOM操作改变元素里面的内容、属性等

### (1) 操作元素内容

- `element.innerText` —— 不识别HTML标签，同时空格和换行也会去掉

- `element.innerHTML` —— 识别HTML标签，保留空格和换行

```html
<p>
  我是文字
  <span>123</span>
</p>
<script>
  let p = document.querySelector('p');
  console.log(p.innerText);//我是文字123
  console.log(p.innerHTML);//【原本格式导出】
</script>
```

### (2) 操作常见元素属性

修改 src、href、title等属性

```html
<button id="ldh">刘德华</button>
<button id="zxy">张学友</button>
<img src="images/ldh.jpg" alt="" title="刘德华">
<script>
  let zxy = document.getElementById('zxy');
  let img = document.querySelector('img');
  
  zxy.onclick = function() {
    img.src = 'images/zxy.jpg';
    img.title = '张学友';
  }
</script>
```

### (3) 操作表单元素属性

DOM操作表单属性： type | value | checked | selected | disabled

```html
<button>按钮</button>
<input type="text" value="输入内容">
<script>
	let btn = document.querySelector('button');
  let input = document.querySelector('input');
  
  btn.onclick = function() {
    imput.value = '被点击了';
    this.disabled = true;
  }
</script>
```

### (4) 操作元素样式属性

​		—— js修改产生行内样式，权重更高

- element.style               行内样式操作   => 针对样式较少、功能简单
- Element.className    类名样式操作【单独写一个类，将当前元素类名修改，覆盖原先类名】

### (5) 操作自定义属性

- **获取**属性值
  - element.属性 —— 获取内置属性值（元素本身自带的属性）
  - element.getAttribute('属性'); —— 获取**自定义属性**

- **设置**属性值
  - element.属性 = '值';     
  - element.getAttribute('属性' , '值'); 
- **移除**属性
  - element.removeAttribute('属性');

```js
//针对内置属性
div.id = 'test';
div.className = 'navs';

//针对自定义属性
div.setAttribute('index',2);
div.setAttribute('class','footer');
```

### (6) H5自定义属性

自定义属性的目的：保存并使用数据，有些数据可以保存到页面中而不用保存到数据库中

- **设置**H5自定义属性

  **data- 开头** 作为属性名并赋值

  ```html
  <div data-index="1"></div>
  
  <script>
  	element.setAttribute('data-index',2);
  </script>
  ```

- **获取**H5自定义属性

  驼峰命名法 :   data-**list-name** => element.dataset.**listName**

  - 兼容性获取 ： `element.getAttribute('data-index');`
  - 【H5新增】：`element.dataset.index` 或 `element.dataset['index'];`



## ⚠️ 排他思想

如果有同一组元素，想要某一元素实现某种样式，需要用到循环的排他思想

- ① 所有元素全部清除样式
- ② 给当前元素设置样式

注意顺序不能颠倒，先干掉其他人，再设置自己

```js
let btns = document.getElementByTagName('button');

for(let i=0; i<btns.length; i++) {
  btns[i].onclick = function() {
    //先把所有按钮去掉背景颜色
    for(let i=0; i<btns.length; i++) {
      btns[i].style.backgroundColor = '';
    }
    //设置当前元素背景颜色
    this.style.backgroundColor = 'pink';
  }
}
```



## 4.节点操作	

​		—— 利用节点层级关系获取元素 （利用**父子兄弟节点关系**获取元素）

### (1)节点层级

#### ① 父级节点 parentNode

`node.parentNode` —— 返回**最近一个的父节点**，没有则返回null

#### ② 子节点 childNode

- `parentNode.childNodes` —— 返回包含指定节点的**子节点集合**（包含所有子节点，<u>包括元素节点、文本节点等</u>）

- 🌟`parentNode.children` —— 只读属性，只返回**所有的子<u>元素</u>节点**

  ```text
  -  既没有兼容性问题，又返回第一个子元素节点  =>  element.children[0]
  
      											最后			   		 element.children[element.children.length-1]
  
  ```

- `parentNode.firstChild` —— 获取**第一个子节点**（包含所有子节点，<u>包括元素节点、文本节点等</u>）
- `parentNode.lastChild`   —— 获取**最后一个子节点**（包含所有子节点，<u>包括元素节点、文本节点等</u>）

- `parentNode.firstElementChild` ——获取**第一个子<u>元素</u>节点 **【兼容性问题】

- `parentNode.lastElementChild` ——获取**最后一个子<u>元素</u>节点** 【兼容性问题】

#### ③ 兄弟节点

- `node.nextSibling` —— **下一个兄弟节点**（包含所有子节点，<u>包括元素节点、文本节点等</u>）

- `node.previousSibling` —— **上一个兄弟节点**（包含所有子节点，<u>包括元素节点、文本节点等</u>）

- `node.nextElementSibling` —— **下一个兄弟<u>元素</u>节点**  【兼容性问题】

- `node.previousElementSibling` —— **上一个兄弟<u>元素</u>节点**  【兼容性问题】

### (2)创建|添加|删除|复制节点

- 动态**创建**元素节点 —— `document.createElement('tagName')`

  ```js
  let li = document.createElement('li');
  ```

- **添加**节点

  - 后面添加 `node.appendChild(child)`（类似于after伪元素）
  - 前面添加`node.insertBefore(child,指定插到该元素之前)`（类似于before伪元素）

  ```js
  let ul = document.querySelector('ul');
  let li1 = document.createElement('li');
  let li2 = document.createElement('li');
  
  ul.appendchild(li1);
  ul.insertBefore(li2,ul.children[0]);
  ```

- **删除**节点 ——  `node.removeChild(child)`

  ```js
  ul.removeChild(ul.children[0]);
  ```

- **复制**节点 —— `node.cloneNode()` 

  - **浅拷贝** （参数为**false**）—— **只克隆复制节点本身**，不克隆里面的子节点

  - **深拷贝** （参数为**true**） —— **复制节点本身及里面所有的子节点**



## ⚠️ 三种动态创建元素的区别

```js
//1.document.write() 
//若页面文档流加载完毕，在调用这句话会导致页面重绘
let btn = document.querySelector('button');
btn.onclick = function() {
  document.write('<div>123</div>');
}

//2.innerHTML创建元素  ——  创建多个元素效率更高，结构稍微复杂
let inner = document.querySelector('.inner');
let arr = [];
for(let i=0; i<=100; i++) {
  arr.push('<a href="#">百度</a>');
}
inner.innerHTML = arr.join('');

//3.document.createElement()创建元素  ——  创建多个元素效率稍低，但结构更清晰
let create = document.querySelector('.create');
for(let i=0; i<=100; i++) {
  let a = document.createElement('a'); 
  create.appendChild(a);
}
```



# 三、DOM重点核心

## 1.注册事件（绑定事件）

​		—— 给元素添加事件

- **addEventListener 事件监听**

`eventTarget.addEventListener(type,listener[,useCapture])`

—— 将指定的监听器注册到eventTarget上，当对象触发指定事件时，就会执行事件处理函数

```js
//注意：事件类型不用添加on
btns[1].addEventListener('click',function() {
  alert(22);
});
```

## 2.删除事件（解绑事件）

- **removeEventListener 事件监听**

`eventTarget.removeEventListener(type,listener[,useCapture])`

```js
divs[1].addEventListener('click',fn);
function fn() {
  alert(22);
	divs[1].removeEventListener('click',fn)
}
```

## 3.DOM事件流

—— 从页面中接收事件的顺序，事件发生时会在元素节点之间按照**特定的顺序传播**

① 捕获阶段

② 当前目标阶段

③ 冒泡阶段

```text
▪︎ js中只能执行 捕获 或 冒泡 其中的一个阶段
▪︎ onclick 和 attachEvent 只能得到冒泡阶段
▪︎ addEventListener(type,listener[,useCapture])第三个参数如果是true，表示在事件捕获阶段调用事件处理程序
▪︎ 实际开发中更关注 事件冒泡
▪︎ 有些事件是没有冒泡的 如onblur、onfocus、onmouseenter、onmouseleave
▪︎ 事件冒泡有时候会带来麻烦，有时候又会帮助很巧妙地做某些事情
```

## 4.事件对象

​		event —— 事件发生后，**跟事件相关的一系列信息数据的集合**都放在这个这个对象里面，有很多属性和方法

- **使用语法**（形参）

  指向**触发事件的对象**

  ```js
  eventTarget.onclick = function(event) {
  }
  
  eventTarget.addEventListener('click',function(event){
    
  })
  ```

- 常见**属性与方法**

  ```text
  e.target                   返回触发事件的对象
  e.type                     返回事件的类型（click、mouseover等）
  e.preventDefault           阻止默认事件（默认行为）比如不让链接跳转
  e.stopPropagation          阻止冒泡
  ```

## 5.事件委托

（事件代理、事件委派）

- **原理**

  —— 不是每个子节点单独设置事件监听器，而是**事件监听器设置在其父节点上**，然后利用**冒泡原理**影响每个子节点

## 6.常用鼠标事件

```text
e.clientX                   返回鼠标相对于 浏览器窗口可视区 的X坐标
e.clientY                   返回鼠标相对于 浏览器窗口可视区 的Y坐标
e.pageX                     返回鼠标相对于 文档页面 的X坐标 【IE9+支持】
e.pageY                     返回鼠标相对于 文档页面 的Y坐标 【IE9+支持】
e.screenX                   返回鼠标相对于 电脑屏幕 的X坐标 
e.screenY                   返回鼠标相对于 电脑屏幕 的Y坐标
```

## 7.常用键盘事件

```text
onkeydown                   某个键盘按键被 按下 时触发
onkeypress                  某个键盘按键  被按下 时触发（不识别功能键，如箭头、shift等）【取分大小写】
onkeyup                     某个键盘按键被 松开 时触发        
```

- 键盘事件对象

  —— keyCode ： 返回该键的ASCII值



# 四、BOM

（Browser Object Model）

—— **浏览器对象模型**，提供独立于内容而**与浏览器窗口**进行交互的对象，核心对象是**window**

缺乏标准，最初是Netscape浏览器标准的一部分（浏览器厂商在各自浏览器上定义的，兼容性较差）

- BOM包含DOM
- window.name特殊属性

## 1.window对象的常见事件

### (1)窗口加载事件

-  load

  —— 当文档内容全部加载完毕（包括DOM元素、图像、flash、CSS等）

  ```js
  window.onload = function() {}   //只能写一次，若有多个则以最后一个为准
  
  window.addEventListener("load",function() {}) //没有次数限制
  ```

- DOMContentLoaded （**速度更快**）

  —— 当DOM加载完成（不包括CSS、图片、flash等）【IE9+】

### (2)调整窗口大小事件

- resize

  —— 窗口大小发生像素变化时

  ```js
  window.onresize = function() {}   
  
  window.addEventListener("resize",function() {}) 
  ```

## 2.定时器

### (1)setTimeout()

​	—— 需要等待一段时间才调用

`window.setTimeout( function(){}, [延迟的毫秒数] )`

- **停止定时器** clearTimeout()

  `window.clearTimeout( timeoutID )`

### (2)setInterval()

​	—— 重复调用一个函数，每隔这个时间，就去调用一次回调函数

`window.setInterval( function(){}, [间隔的毫秒数] )`

- **停止定时器** clearInterval()

  `window.clearInterval( timeoutID )`

### ⚠️ 二者注意与区别

- 注意

  - 调用函数 —— 直接写函数｜函数名（不用加括号）

  - window可以省略

  - 定时器可能有很多，因此常给定时器赋一个标识符

- 区别
  - setTimeout() 只**调用一次就结束**
  - setInterval()  **调用很多次**，每隔一段时间就会调用一次



## 3.this

一般情况下，this最终指向的是调用它的对象

- ① 指向**window**

  ​		—— 全局作用域或普通函数中，this指向全局对象window

  ```js
  //1.
  console.log(this);
  
  //2.
  function fn() {
    console.log(this);
  }
  window.fn();
  
  //3.
  window.setTimeout(function(){
    console.log(this);
  },1000)
  ```

- ② 指向**方法调用者**

  ​	—— 方法调用中谁调用this指向谁

  ```js
  //1.
  let o = {
    sayHi: function() {
       console.log(this);//指向o对象
    }
  }
  o.sayHi();
  
  //2.
  let btn = document.querySelector('button');
  btn.addEventListener('click',function() {
     console.log(this);//指向btn这个按钮对象
  })
  ```

- ③ 指向**构造函数中的实例对象**

  ​    —— 构造函数中this指向构造函数的实例

  ```js
  function Fun() {
     console.log(this);//指向fun实例对象
  }
  let fun = new Fun();
  ```

## 4.location对象

​		—— 获取或设置**窗体的URL**，可以用于解析URL

### (1)URL

（Uniform Resource Locator）互联网上标准资源的地址

`protocol://host[:port]/path/[?query]#fragment`

```text
protocol              通信协议   （常用http、ftp、maito等）
host                  主机（域名） 如www.baidu.com
port                  [端口号]    默认80
path                  路径        由“/”隔开的字符串，一般用来表示主机上的一个目录或文件地址
query                 参数        以键值对形式，通过“&”隔开
fragment              片段        #后面的内容（常见于链接、锚点）
```

### (2)location对象的属性

```text
location.href          获取或设置 整个URL
location.search        返回 参数
location.host          返回 主机（域名）
location.port          返回 端口号
location.pathname      返回 路径
location.hash          返回 片段（#后面的内容）
```

### (3)location对象的方法

```text
location.assign()      跟href一样，可以跳转（重定向）页面 （可以后退页面）
location.replace()     替换当前页面（不记录历史，不可以后退页面）
location.reload()      重新加载页面，相当于 刷新     
```

## 5.navigator对象

包含浏览器的信息，常用**属性userAgent** —— 返回由客户机发送服务器的user-agent头部的值

## 6.history对象

—— 于浏览器历史记录进行交互

```text
back()                  后退
forward()               前进
go(参数)                前进或后退（参数1 表示前进1个页面；参数-1 表示后退1个页面）
```

## 7.三大系列

### (1)元素偏移量 offset系列

常用属性

```text
element.offsetParent             返回该元素带有【定位】的父级元素，若父级都没有定位则返回body
element.offsetTop                返回该元素相对 带有【定位】的父级元素 上方的偏移
element.offsetLeft               返回该元素相对 带有【定位】的父级元素 左边框的偏移
element.offsetWidth              返回自身 包括padding、边框、内容去的宽度【不带单位】
element.offsetHeight             返回自身 包括padding、边框、内容去的高度【不带单位】
```

#### ⚠️offset与style的区别

```text
					offset            													style
					
可以获得【任意样式表】的样式值      			  			只能得到【行内样式表】的样式值
		获得的数值【没有单位】													获得【带有单位】的字符串
offsetWidth【包含padding+border+width】			 offsetWidth【不包含padding+border+width】	
		offsetWidth等属性是【只读属性】								offsetWidth等属性是【可读写属性】
		 【🌟获取元素大小位置】														【🌟给元素改值】
```



### (2)元素可视区 client系列

常用属性

```text
element.clientTop                返回元素 上边框 的大小
element.clientLeft               返回元素 左边框 的大小
element.clientWidth              返回自身 包括padding、内容区的宽度【不含边框、不带单位】
element.clientHeight             返回自身 包括padding、内容区的高度【不含边框、不带单位】
```

### (3)元素滚动 scroll系列

常用属性

```text
element.scrollTop                返回 被卷去的 上侧距离【不带单位】
element.scrollLeft               返回 被卷去的 左侧距离【不带单位】
element.scrollWidth              返回自身 实际的宽度【不含边框、不带单位】
element.scrollHeight             返回自身 实际的高度【不含边框、不带单位】
```

### 🌟 三大系列总结

```text
▪︎ offset   获取元素【位置】		
	▫︎ offsetWidth 返回自身 包含padding、边框、内容区 的宽度 
	
▪︎ client   获取元素【大小】
	▫︎ clientWidth 返回自身 包含padding、内容区 的宽度，【不含边框】
	
▪︎ scroll   获取【滚动距离】
	▫︎ scrollWidth 返回 自身实际 的宽度，【不含边框】
```

- 页面滚动距离 window.pageXOffset



## 🌰 mouseenter和mouseover的区别

```text
					mouseenter																mouseover
					【不会冒泡】
	鼠标经过自身盒子会触发，经过子盒子还会触发    				只会经过自身盒子触发
```



# 五、JS执行机制

- JS是**单线程**

  —— 同一时间只能做一件事，前一个任务结束，才开始执行后一个任务

## 1.同步和异步

- 同步

  —— 前一个任务结束后再执行后一个任务，程序的**执行顺序与任务排列顺序是一致的**

  ```text
  任务在主线程上执行，形成一个 **执行栈**
  ```

- 异步

  —— 在做一件事的同时，还可以处理其他事

  ```text
  通过 **回调函数** 实现，如：
  
  	- 普通事件 click、resize等
  	- 资源加载 load、error等
  	- 定时器     setTimeout、setInterval等
  ```

​		异步任务相关**回调函数**添加到**任务队列**中

## 2.执行机制

- ① 先执行执行栈中的**同步任务**
- ② 异步任务（回调函数）放入任务队列中 
- ③ 执行完所有同步任务后，系统按序读取任务队列中的**异步任务**，被读取的异步任务**结束等待状态**，**进入执行栈，开始执行**

<p style="color:rgb(91, 137, 237);font-size:25px;">事件循环</p>

```text
主线程不断重复获得任务、执行任务，这一机制被称为事件循环（event loop）
```



