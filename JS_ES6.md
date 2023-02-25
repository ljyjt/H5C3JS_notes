# 一、ES6

（ECMAScript）—— 由ECMA国际标准化组织制定的一项**脚本语言的标准化规范**

【ES6为**ES2015及后续版本**】

## 🌰 为什么使用ES6

```text
每一次标准的诞生都意味着语言的完善，功能的加强。JS语言也有令人不满意的地方：
① 变量提升特性增加了程序运行时的不可预测性；
② 语法过于松散，实现相同的功能，不同的人可能会写出不同的代码

▪︎ ES6版本变动内容最多，具有里程碑意义
▪︎ ES6加入了很多语法特性，编程实现更简单、高效
▪︎ 前端开发趋势，就业必备技能
```



# 二、ES6新增语法

## 1.let、const

### (1)let

—— ES6新增**声明变量**的关键字

- ① **块级作用域**
  - 使用**let**关键字在{}中声明变量才具有**块级作用域**
  - 使用**var**声明的变量**不具备块级作用域**
- ② 不存在**变量提升**
- ③ 暂时性死区
- ④ **不影响作用域链**

### 🌰 let经典面试题

```js
let arr = [];
for(var i = 0; i<2; i++) {
		arr[i] = function() {
				console.log(i);
		}
}
arr[0]();//2
arr[1]();//2

//🌟每次循环都会产生一个块级作用域，每个块级作用域中的变量是不同的
let arr = [];
for(let i = 0; i<2; i++) {
		arr[i] = function() {
				console.log(i);
		}
}
arr[0]();//0
arr[1]();//1
```

### (2)const

—— 声明常量（值｜内存地址不能变化的量）

- ① 具有**块级作用域**
- ② **声明常量是必须赋值**（常量名大写）
- ③ 常量**赋值后不能修改**

## 🌰 let|const|var区别

```text
		var               let                const 
	函数作用域         块级作用域            块级作用域
	 变量提升         不存在变量提升        不存在变量提升
  值可以修改          值可以修改          值不可以修改
   重复声明          不可重复声明          不可重复声明
```

## 2.解构赋值

### (1)数组解构

—— 按照一一对应的关系从数组中提取值，并将值赋给变量

【解构不成功，变量值为undefined】

```js
let [a,b,c] = [1,2,3];
console.log(a);//1
console.log(b);//2
console.log(c);//3
```

### (2)对象解构

—— 使用变量名字匹配对象属性，匹配成功将对象属性的值赋给变量

```js
let person = {name: 'zhangsan', age: 20};

//①
let {name, age} = person;
console.log(name);//'zhangsan'
console.log(age);//20

//②myName|myAge属于别名
let {name: myName, age: myAge} = person;
console.log(myName);//'zhangsan'
console.log(myAge);//20
```

## 3.箭头函数

`() => {}`

`const fn = ()=> {}`

—— **适合与this无关的回调**（定时器、数组方法等）；

​		不适合与this有关的回调（如事件回调、对象方法等）

- ① 函数体只有一句代码，且代码的执行结果就是返回值，可以省略大括号

- ② 形参只有一个，可以省略小括号
- ③ 箭头函数不绑定this，**this**指向**函数定义位置的上下文**
- ④ 不能作为构造函数实例化对象
- ⑤ 不能使用arguments变量

### 🌰 对象的this指向

```js
//【对象的作用域为window，因此对象内的this指向window】
let obj = {
  age: 20,
  say: () => {
    alert(this.age);
  }
}
obj.say(); //undefined
```

## 4.剩余参数 rest

—— 将**不定数量的参数**表示为一个**数组**

```js
function sum(first,...args) {
  console.log(first);  //10
  console.log(...args);//[20,30]
}
sum(10,20,30);
```

### 🌰 剩余参数与解构配合使用

```js
let students = ['ljy','ljc','jt'];
let [s1,...s2] = students;
console.log(s1);//ljy
console.log(s2);//['ljc','jt']
```

## 5.数组的扩展方法

### (1)扩展运算符

#### ① 合并数组

```js
//方法一
let arr1 = [1,2,3];
let arr2 = [3,4,5];
let arr = [...arr1,...arr2];
//方法二
let arr = arr1.push(...arr2);
```

#### ② 类数组转变为真正数组

```js
let oDivs = document.getElementsByTagName('div');//伪数组

//方法一
oDivs = [...oDivs];
//方法二  Array.from()
oDivs = Array.from(oDivs);
```

#### ④ 数组克隆

```js
let arr = [1,2,3];
let arr1 = [...arr];
```

### (2)find()

### (3)findIndex()

### (4)includes()

## 6.字符串的扩展方法

### (1)模版字符串

#### ① 解析变量

```js
let name = '张三';
let sayHello = `Hello,my name is ${name}`;//Hello,my name is 张三
```

#### ② 换行

```js
let html = `<div>
		<span>1</span>
		<span>2</span>
		<span>3</span>
</div>`;
```

#### ③ 调用函数

```js
const sayHello = function() {
  return '123';
}
let greet = `${sayHello()}哈哈哈哈`;
console.log(greet);//123哈哈哈哈
```

### (2)startsWith()与endsWith()

```js
let str = 'Hello world!';
str.starsWith('Hello');//true
str.endsWith('!');//true
```

### (3)repeat()

—— 将原字符串重复n次，返回一个新字符串

```js
'x'.repeat(3);//'xxx'
'hello'.repeat(2);//'hello hello'
```

## 7.set数据结构

—— 类似于数组，但**成员的值都是唯一**的，没有重复的值

- Set是一个**【构造函数】**：生成Set数据结构

  `const s= new Set();`

- 可以接收一个数组作为参数，用来初始化

  `const set = new Set([1,2,3,4,4]);`//可以给**数组去重**

### (1)实例方法

```
add(val)                 添加某个值，返回【Set结构本身】
delete(val)              删除某个值，返回一个【布尔值】
has(val)                 返回【布尔值】
clear()                  清除所有成员，没有返回值
```

### (2)遍历 forEach()

## 8.简化对象写法

```js
let name = 'ljy';
let change = function() {...};
                         
const obj = {
  name,
  change,
  improve(){
    ...
  }//对象内定义方法可以省略function
}
```

## 9.默认参数值

- 允许给函数的**参数赋初始值**

  ```js
  function add(a,b,c=10) {
    return a+b+c;
  }
  console.log(add(1,2));//1+2+10=13
  ```

- 与**解构赋值结合**

  ```js
  function connect({host="127.0.0",username,password,port}) {
    ...
  }
  connect({
    host: 'atguigu.com',
    username: 'root',
    password: 'root',
    port: 3306
  })
  ```

## 10.Symbol()

—— ES6引入的新的**原始数据类型**，表示**独一无二的值**

- **创建**Symbol（内部实现唯一性）

  - ① `let s = Symbol();`

  - ② `let s = Symbol('注释');` 【注释一致，不相等】

  - ③ `let s = Symbol.for('注释')`【注释一致，相等】

- **作用**：安全地给对象添加属性、方法（**避免命名冲突**）

  ```js
  let methods = {
    up: Symbol(),
    down: Symbol()
  };
  
  let game = {
    name: '狼人杀',
    [Symbol('say')]: function() {...}
  }
    
  game[methods.up] = function() {...}
  ```

  

