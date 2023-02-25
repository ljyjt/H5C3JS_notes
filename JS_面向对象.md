# 一、面向对象

OOP（Object Oriented Programming）

—— 把事务分解成一个个对象，由对象之间分工与合作

以**对象功能**划分问题，而不是步骤

- 特性
  - 封装性
  - 继承性
  - 多态性

- 优缺点
  - 优点
    - 易维护、易复用、易扩展，使系统更灵活、易于维护
  - 缺点
    - 性能比面向过程低



# 二、【ES6】中的类和对象

面向对象的思维特点：

- ① 抽取（抽象）对象**共用的属性和行为**组织（封装）成一个**类（模版）**
- ② 对 类 进行**实例化**，获取类的对象

## 1.对象

JS中，对象是**一组无序的相关属性和方法的集合**，所有的事物都是对象

- 对象的**构成**
  - 属性 —— 事物的**特征**
  - 方法 —— 事物的**行为**

## 2.类 class

- 类 —— **抽象了对象的公共部分**，泛指某一大类（class）

- 对象 —— **特指某一个**，通过 **类实例化** 一个具体对象

```text
① 先有类，才能实例化 => 实例化要在类的下面
② 类里面 【共有的属性和方法】 一定要加 this 使用
```

### (1)创建类

```js
//创建类
class Name {
  //class body
}

//new实例化对象
let xx = new Name();
```

### (2)constructor 构造函数

—— 将**类共有的属性**放进构造函数，new生成实例时自动调用该函数（如果没有定义，类内部会自动给我们创建一个constructor()）

```js
class Star {
  constructor(uname,age) {
    this.uname = uname;
    this.age = age;
  }
}
```

- 只要实例化对象就会自动调用constructor

  => 可以在构造函数内调用方法，即能够以实例化就调用方法（注：加this）

### (3)添加方法

```js
class Star {
  constructor(uname,age) {
    this.uname = uname;
    this.age = age;
  }
  //添加方法
  sing() {
    ....
  }
}
```

- 类里所有函数不需要加 function
- 多个函数方法之间不用加 ","分割

### (4)类的继承

#### ① extends

—— 子类继承父类的一些属性和方法

```js
class Father {}
class Son extends Father {
  //子类继承父类
}
```

#### ② super关键字

—— **访问和调用对象父类上的函数**，可以调用父类的构造函数，也可以调用父类的普通函数【就近原则】

```js
class Father {
  say() {
    console.log('我是爸爸');
  }
  plus(x,y) {
    return x+y;
  }
}

class Son extends Father {
  constructor(x,y) {
    super(x,y); //⚠️在constructor内 super必须在子类this之前调用
    this.x = x;
    this.y = y;
  }
  say() {
    super.say();//⚠️调用父类的say方法
  }
}

let demo = new Son();
demo.say(); //输出”我是爸爸“
console.log(demo.plus(1,2)); //输出 3
```



## ⚠️ 三个注意点

```text
① ES6没有变量提升，所以必须先定义类，才能通过类实例化对象
② 类里面的共有属性和方法一定要加 this 使用
③ 注意类里面的 this指向 问题
		—— constructor里的this => 指向实例对象
		           方法里的this =>指向这个方法的调用者
```



# 三、构造函数和原型

**【ES6之前】，对象不是基于类创建的，而是用构造函数的特殊函数来定义对象和它们的特征**

## 1.构造函数

<p style="color:rgb(95, 206, 114);font-size:20px;"> => 公共属性</p>

—— 把对象中一些公共的属性和方法抽取出来，封装到这个函数里面

- 注意
  - 构造函数用于**创建某一类对象**，**首字母大写**
  - 构造函数要和 **new** 一起使用

```js
function Star(uname,age) {
  this.uname = uname;
  this.age = age;
  
  this.sing = function() {
    console.log('我会唱歌');
  }
}

let ldh = new Star('刘德华',18);
ldh.sing();//输出“我会唱歌”
```



### 🌟 new在执行时会做四件事情

```text
① 在内存中创建一个新的空对象
② 让this指向这个新对象
③ 执行构造函数里的代码，给这个新对象添加属性和方法
④ 返回这个新对象【构造函数里不需要return】
```

###  静态成员 & 动态成员

- 静态成员

  —— 在**构造函数本身**上添加的成员：只能由**构造函数本身**访问

- 动态成员

​		—— 在**构造函数内部**创建的对象成员：只能由**实例化对象**来访问

```js
function Star(uname,age) {
  this.uname = uname;
  this.age = age;
  this.sing = function() {
    console.log('我会唱歌');
  }
}
let ldh = new Star('刘德华',18);

//1.动态成员uname|age|sing()由this添加，只能通过实例化对象来访问
ldh.sing();

//2.静态成员sex通过构造函数Star添加，只能通过Star构造函数调用
Star.sex = '男';
console.log(Star.sex);//可以
console.log(ldh.sex);//不行
```

## 2.原型对象 prototype

<p style="color:rgb(95, 206, 114);font-size:20px;"> => 公共方法</p>

（每一个**构造函数**都有一个prototype属性）

—— prototype对象的所有属性和方法都会被构造函数所拥有

​						 => 可以把**不变的方法，直接定义在prototype对象上**，这样所有对象实例都可以**共享这些方法**

## 3.对象原型 _ proto _

（**对象**都有一个_ proto _属性） => 指向构造函数的prototype原型对象

—— 为**对象的查找机制提供一个方向**（非标准属性）



### 🌟 构造函数｜实例｜原型对象 的关系

<img src="/Users/ljy/Desktop/H5C3_notes/构造函数｜实例｜原型对象关系.jpeg" alt="构造函数｜实例｜原型对象关系" style="zoom:50%;" />



### 🌟 原型链

<img src="/Users/ljy/Desktop/H5C3_notes/原型链.jpeg" alt="原型链" style="zoom:60%;" />



## 4.JS的成员查找机制（规则）

① 当访问一个对象的属性或方法时，首先查找这个**对象自身**有没有该属性

② 如果没有就**查找它的原型**（_ proto_指向的prototype对象）

③ 如果还没有就查找**原型对象的原型**（Object的原型对象）

④ 以此类推，一直找到Object为止（null）



### 🌟 原型对象this指向

**构造函数**、**原型对象**函数里的this => 指向**对象实例**



## 5.继承

—— 通过**构造函数+原型对象**模拟实现继承 => **组合继承**

### call()

—— 调用这个函数，并修改函数运行时的this指向

`fun.call(thisArg,arg1,arg2,...)`

- thisArg : 当前调用函数this的指向对象
- arg1，arg2：传递的其他参数

```js
function fn(x,y) {
  console.log(this);//指向对象o
  console.log(x + y);//3
}
let o = {
  name: 'andy'
}

fn.call(o,1,2);//🌟 将fn的this指向对象o，并传入两个参数
```

## 6.类的本质

**ES6里的类 => 【语法糖】**

- class本质 => function，构造函数的另一种写法
- 类的所有方法都定义在类的prototype属性上
- 类创建的实例，里面也有_ proto _指向类的prototype原型对象



# 🌰 Object.defineProperty()

—— 定义对象中的新属性 或 修改原有的属性

`Object.defineProperty(obj,prop,descriptor)`

- obj：目标对象
- prop：需定义或修改的属性的名字
- descriptor：目标属性所拥有的特性

```js
Object.defineProperty(obj,'num',{
  value: 1000;        //设置属性的值                       【默认undefined】
  writable: false;    //值是否可以 重写                    【默认false】
  enumerable: false;  //目标属性是否可以 被枚举              【默认false】
  configurable: false;//目标属性是否可以 被删除 或 再次修改特性【默认false】
})
```

