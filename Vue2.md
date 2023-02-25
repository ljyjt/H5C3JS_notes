# 一、Vue

—— 动态构建用户界面的**渐进式**Javascript框架

- 特点
  - 遵循**MVVM**模式
  - 采用**组件化**模式，提高代码复用率，让代码更好维护
  - **声明式**编码，让编码人员**无需直接操作DOM**，提高开发效率
  - 利用**虚拟DOM +** 优秀的 **Diff算法**，尽量复用DOM节点

- 与其他JS框架的关联
  - 借鉴Angular的**模版**和**数据绑定**技术
  - 借鉴React的**组件化**和**虚拟DOM**技术

## 1.创建Vue实例

```js
new Vue({
  el: '#root',//el指定当前Vue实例为哪个容器服务
  data: {
    name: 'ljy'
  }
})
```

### 生命周期

<img src="/Users/ljy/Desktop/H5C3_notes/Vue生命周期.jpeg" alt="Vue生命周期" style="zoom:70%;" />

## 2.模版语法

**内部是js表达式，且可以读取到data中的所有属性**

### (1)插值语法

—— 解析**标签体内容**

- **文本**

  - 最常见形式： `{{}}`
    - 当绑定数据上的值发生变化时，插值处的内容会更新

  - `v-once`：一次性地插值，当数据改变时，插值处的内容不会更新

- **js表达式**

  ⚠️ 区分**js表达式**与**js代码（语句）**

  ```text
  ▪︎ js表达式
  		—— 一个表达式会产生一个值，可以放在任何一个需要值的地方
  	a
  	a+b
  	demo(1)
  	x===y?'a':'b'
  		
  ▪︎ js代码
  		—— 控制代码走向
  	if() {}
  	for() {}
  	var a = 1
  ```

### (2)指令语法 `v-`

—— 解析**标签**（包括标签属性、标签体内容、绑定事件...）

- **条件渲染**

  - `v-if="表达式"`**【切换频率较低】**

    —— 条件不成立时，v-if所有子节点不会解析

    - **不展示的DOM元素直接<u>被移除</u>**（元素可能无法获取到）
    - v-if可以和v-else-if、v-else一起使用，但要求结构不能被打断

  - `v-show="表达式"` **【频繁切换】**

    - **不展示的DOM元素<u>未被移除</u>**，只是使用样式隐藏掉（元素一定可以获取到）

- **列表渲染**

  `v-for="(item,index) in xxx" :key="yyy"`

  —— 用于展示列表数据

  - key最好使用数据的**唯一标识**

- `v-on:xxx`|`@xxx` （事件监听）



## 3.数据绑定

### (1)单向数据绑定

`v-bind:href="xxx"` | `:href`

- 数据只能**从data流向页面**

### (2)双向数据绑定

`v-model:value="xxx"`（用于**表单类**/输入类的元素，🈶️value值） | `v-model="xxx"`(默认收集**value值**)

- 数据不仅**能从data流向页面**，还能**从页面流向data**



## 4.MVVM模型

Vue虽然没有完全遵循MVVM模型，但是受到了其启发

- **M**：模型（Model）—— 对应data中的数据

- **V**：试图（View）—— 模版【DOM】
- **VM**：视图模型（ViewModel）—— Vue实例对象

```text
① data中所有的属性，最后都出现在vm身上
② 【vm身上的所有属性】及【Vue原型上的所有属性】，在Vue模版中都可以直接使用
```



## 5.数据代理

—— **通过一个对象代理对另一个对象中属性的操作**（读/写）

- ① Vue中的数据代理

  ——通过**vm对象代理data对象中属性的操作**

  ```js
  let obj = {x: 100}
  let obj2 = {y: 200}
  Object.defineProperty(obj2,'x',{
    get() {
      return obj.x;
    },
    set(val) {
      obj.x = val;
    }
  })
  ```

- ② Vue中数据代理的**好处**

  ——**更加方便地操作**data中的数据

- ③ 基本原理

  - 通过Object.defineProperty()把data对象中所有属性添加到vm上
  - 为每一个添加到vm上的属性都指定一个getter和setter
  - 在getter和setter内部去操作（读/写）data中对应的属性

  ```text
  Object.defineProperty(obj,prop,description)
  
  ▪︎ obj-目标对象
  ▪︎ prop-需定义或修改的属性名
  ▪︎ descriptor-目标属性拥有的特性
  ```

  ```js
  let num = 18;
  let person = {
    name: '张三',
    sex: '男'
  }
  Object.defineProperty(person,'age',{
    get() {
      console.log('有人读取age属性了');
      return num;
    },
    set(val) {
      console.log('有人修改了age属性，且值是',val);
      number = val;
    }
  })
  ```



## 6.computed与watch

- computed**计算属性**
  - ① 要显示的数据不存在，通过已有属性计算得来
  - ② 在computed对象中定义计算属性
  - ③ 再页面中使用 {{方法名}} 显示计算结果

- watch**监视属性**
  - 属性变化时，回调函数自动调用，在函数内部进行计算
  - 监视属性必须存在才能监视

### 🌟 computed与watch的区别

```text
computed能完成的功能watch都可以完成
watch能完成的功能，computed不一定能完成【如watch能进行异步操作】、
```



