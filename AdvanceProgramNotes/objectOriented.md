# 面向对象的程序设计

> ECMA-262把对象定义为：“无序属性的集合，其属性可以包含基本值、对象或者函数。”严格来讲，这就相当于说对象是一组没有特定顺序的值。（每个属性或方法都一个名字，而每个名字都映射到一个值）


## 理解对象

> 创建对象最简单的方式就是创建一个Object的实例，然后再为它添加属性和方法；也可以使用对象字面量成为创建对象的首选模式。

```javascript
var obj = new Object();
obj.name = "jame";
obj.age = 23;
obj.job = "software Engineer";
obj.sayName =  function(){
  console.log(this.name);
};


//字面量方法
var obj2 = {
  name:'jame',
  age:23,
  job:'software Engineer',
  sayName :function(){
    console.log(this.name);
  }
};

```

###1. 属性类型

>  ECMAScript第5版在定义只有内部采用的特性（attribute）时，描述了属性的各种特征。这些特性值只是为了实现javascript引擎用的，因此在javascript中不能直接访问它们。为了表示特性是内部值，该规范把它们放在**两队方括号**中，例如：[[Enumerable]]。
+ 数据属性
+ 访问器属性

####1.1 数据属性

> 数据属性包含一个数据值的位置。在这个位置可以读取和写入值。主要有4个描述其行为的特性：
+ [[Configurable]]:表示能够通过delete删除属性从而重新定义属性，能否修改属性的特性，能够把属性修改为访问器属性。默认值为true
+ [[Enumerable]]: 表示能否通过for-in循环返回属性。默认值为true
+ [[Writable]]: 表示能否修改属性的值。默认值为true
+ [[Value]]:包含这个属性的数据值。读取属性值从该位置读取，写入新增也保存该位置。默认值undefined

```javascript
// 默认情况下[[Configurable]]、[[Enumerable]]、[[Writable]]的值都为true；而[[Value]]的值'Nicholas'
var person = {
  name:'Nicholas'
};
```

***要修改属性默认的特性，必须使用ECMAScript5的Object.defineProperty()方法。正常接收3个参数：***
+ 属性所在的对象
+ 属性名字
+ 属性描述符对象，描述符对象必须是[[Configurable]]、[[Enumerable]]、[[Writable]]、[[Value]]其中的一个或多个，可以修改对应的特性值

```javascript
var person = {};
Object.defineProperty(person, "name", {
  configurable: false,
  value: 'linq'
});

Object.defineProperty(person, "age", {
  writable: false,
  value : 23
});

console.log(person.name);
delete person.name;       //error

console.log(person.age);
person.age = 11;          //error

```

***为age赋值时,由于age是只读的。如果给它指定新值，在严格模式下，赋值报错；非严格模式下，赋值被忽略***



