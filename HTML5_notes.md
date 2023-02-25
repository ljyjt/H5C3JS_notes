# 1.基本概念

## ①网页

- **网站**：在因特网上<u>根据一定的规则</u>，使用HTML等制作的用于展示特定内容相关的<u>网页集合</u>

- **网页：**网站中的“一页”，通常是<u>HTML格式</u>的文件，要通过<u>浏览器阅读</u>

  【构成网站的基本元素（由图片、文字、视频等元素组成），常以.htm/.html后缀，俗称HTML文件】

## ②HTML

<p style="color:rgb(241, 157, 56);font-size:18px">超文本标记语言（Hyper Text Markup Language）</p>

- 描述网页的一种语言【不是编程语言 => **标记语言**（是一套标记标签）】

- 超文本 ：

    ① 超越了文本的限制 

    ② 超级链接文本（从一个文件跳转到另一个文件，与世界各地主机的文件连接）

## ③常用浏览器

- 浏览器内核（渲染引擎） 

  ​		—— 读取网页内容，整理讯息，计算网页的显示方式并显示页面

- ```text
  浏览器           内核
   IE             Trident
   firefox        Gecko
   safari         webkit
   chrome/Opera   Blink(webkit分支，国产浏览器常用的内核)
  ```

## ④Web标准

​        —— 由W3C组织（万维网联盟）和其他一起标准化组织制定的**一系列标准的集合**

- 构成：
  - 结构(Structure)：对**网页元素**进行整理和分类 【HTML】
  - 表现(Presentation): 设置网页元素的版式、颜色、大小等**外观样式** 【CSS】
  - 行为(Behavior): 网页模型的定义及**交互**的编写 【Javascript】



# 2.Html标签

## ①基本结构标签

- 文档类型声明标签`<!DOCTYPE html>`【告诉浏览器使用哪种HTML版本显示网页 => H5版本】

- 根标签 `<html></html>`

  - 头部标签`<head></head>`

    - title标签`<title></title>`【头部标签内一定要设置】

    - 字符集`<meta charset="UTF-8"/>`【文档使用哪种字符编码 => 万国码】

  - 主体标签`<body></body>`

## ②常用标签

- 标题标签：`<h1></h1>  —— <h6></h6>`【独占一行，文字加粗】
- 段落标签：`<p></p>`
- 换行标签：`<br/>`

## ③文本格式化标签

- 粗体 `<strong></strong>` `<b></b>`
- 斜体 `<em></em>` `<i></i>`
- 删除线 `<del></del>` `<s></s>`
- 下划线 `<ins></ins>` `<u></u>`

## ④图像标签

`<img src=""/>`

- 属性：

```text
src        路径【必须属性】
alt        替换文本
title      提示文本
width      宽度
height     高度
border     边框粗细
```

## ⑤超链接标签

`<a href=""></a>`

- 属性：

```text
href        指定链接目标的URL地址【必须属性】
target      指定链接页面的打开方式
					 【_self默认值（替换当前页面），_blank（打开新窗口）】
```

- 链接分类

  - 外部链接：直接链接其他网站url

  - 内部链接：网站内部页面间的相互连接，链接内部页面名称

  - 空链接

  - 下载链接：href里的地址为**文件或压缩包**，下载该文件

  - 网页元素链接：文本、图像、表格等各种网页元素都可以添加超链接

  - 锚点链接：点击链接**快速定位到页面中的某个位置**

    - ```html
      <a href="#two">第二集</a>
      <h2 id="two">第二集介绍</h2>
      ```

## ⑥表格标签

<p style="color:rgb(241, 157, 56);font-size:18px">展示数据</p>

```html
<table>
  <tr>
    <th>表头单元格【加粗并居中显示】</th>
    <td>单元格内文字</td>
  </tr>
</table>
```

- 表格属性

  - ```text
    align         left/center/right      对齐方式
    border        1/""                   是否有边框
    cellpadding   默认1像素               单元边沿与其内容间的空白
    cellspacing   默认2像素               单元格间的空白
    width                                宽度
    ```

- 表格结构标签

  - ```html
    <thead>表格头部区域</thead>
    <tbody>表格主题区域</tbody>
    ```

- **合并单元格**
  - ①先确定**跨行**还是**跨列**（跨行合并：`rowspan=""`       跨列合并：`colspan=""`）
  - ②找到**目标单元格**【跨行最上侧、跨列最左侧】（合并方式=“单元格数量”）
  - ③删除多余单元格

## ⑦列表标签

<p style="color:rgb(241, 157, 56);font-size:18px">布局（css中完成）</p>

- 无序列表【带有**样式属性**】
  - `<ul> <li>列表项1</li> </ul>`
- 有序列表
  - `<ol> <li>列表项1</li> </ol>`
- 自定义列表
  - `<dl> <dt>名词1</dt> <dd>名词1解释1</dd> </dl>`

## ⑧表单标签

<p style="color:rgb(241, 157, 56);font-size:18px">收集用户信息</p>

- 表单域	`<form></form>`

  - 常用属性

    ```text
    action       url地址     
    method       get/post
    name         指定表单名称，区分页面中的多个表单域
    ```

- 表单控件

  - ① input

    - 属性：

      ```text
      type            	类型
      								【button            可点击按钮
      								 	checkbox          复选框
      									radio             单选框
      									password          密码
      									text              单行输入字段
      									file              供文件上传
      									hidden            隐藏的输入字段
      									image             图像形式的提交按钮
      									reset             重置按钮（清除表单所有数据）】
      name              名称（区别不同表单元素）
      value             规定input元素的值
      checked           是否被选中（radio/checkbox）
      maxlength         输入字符的最大长度
      ```

    - `<label>`标签 

      ​					=> 绑定表单元素，点击label标签内的文本时，自动将焦点转到对应的表单元素上

      ```html
      <label for="sex">男</label>
      <input type="radio" id="sex">
      ```

  - ② select （下拉列表）

    - ```html
      <select>
         <option selected>选项1</option>
         <option>选项2</option>
         <option>选项3</option>
         ...
      </select>
      ```

  - ③ textarea （多行文本输入）

    - ```html
      <textarea rows="3" cols="20">
        文本内容
      </textarea>
      ```



# 3.HTML5的新特性

增加一些新标签、新表单、新表单属性

## ①语义化标签

```html
<header>头部标签</header>
<nav>导航标签</nav>
<article>内容标签</article>
<section>定义文档某个区域</section>
<aside>侧边栏标签</aside>
<footer>尾部标签</footer>
```

- 语义化标准主要是**针对搜索引擎**
- 可以使用多次

## ②多媒体标签

```html
<audio>音频</audio>
<video>视频</video> 
```

- 当前只支持三种视频格式：MP4、WebM、Ogg

- **视频video**常见属性

  ```text
  autoplay        autoplay         自动播放（在谷歌浏览器要添加muted）
  controls        controls         向用户显示播放控件
  loop            loop             循环播放
  poster          Imgurl           加载等待的画面
  muted           muted            静音播放
  preload         auto ｜ none     预加载视频（若有autoplay则忽略该属性）
  src             url              url地址
  width           px               宽度
  height          px               高度
  ```

- **音频audio**常见属性

  ```text
  autoplay        autoplay         音频就绪后马上播放
  controls        controls         向用户显示播放控件
  loop            loop             循环播放
  src             url              url地址
  ```

## ③新增input类型

```text
type="number"                 限制用户必须输入数字类型
type="tel"                    手机号码
type="search"                 搜索框
type="email"                  限制用户必须输入Email类型
type="url"                    限制用户必须输入url类型
type="date"                   限制用户必须输入date类型
type="time"                   限制用户必须输入time类型
type="month"                  限制用户必须输入month类型
type="week"                   限制用户必须输入week类型
type="color"                  限制用户必须输入color类型
```

## ④新增的表单属性

```text
required           required           必填
placeholder        提示文本            默认显示，输入文本后就没了
autofocus          autofocus          自动聚焦到指定表单
autocomplete       off ｜ on          用户键入时，浏览器基于之前键入的值，显示出在字段中填写的选项（off安全性更高）
multiple           multiple           多选文件提交
```

