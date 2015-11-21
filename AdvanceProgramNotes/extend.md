# 继承 

> 许多OO语言都支持两种继承方式（接口继承和实现继承）由于函数没有签名，在ECMAScript中无法实现接口继承，只支持实现继承。而实现继承主要是依靠原型链来实现。
+ 接口继承：只继承方法签名。
+ 实现继承：继承实际的方法。


构造函数、原型、实例三者之间的关系：
+ ***每个构造函数都有一个原型属性（指向原型对象的指针）***
+ ***每一个原型对象都有一个指向构造函数的属性***
+ ***每一个实例都有一个指向原型的内部指针***

##1. 原型链

> 原型链基本思想是利用原型让一个引用类型继承另外一个引用类型的属性和方法。

```javascript
function SuperType(){
  this.property = false;
}

SuperType.prototype.getProperty = function(){
  return this.property;
};

function SubType(){
  this.property = true;
}

//此时SubType 继承了SuperType
SubType.prototype = new SuperType();

var instance = new SubType();

```

原型继承关系图如下：
![](images/prototypeextend.png)

### 1.1 别忘记默认的原型

> 事实上，前面的原型连少了一环。我们都知道所有的引用类型都是继承自Object类型，而这个继承也是通过原型链实现的。***所有函数的默认原型都是Object的实例，默认原型都会包含一个内部指针，指向Object.prototype***。

完整原型连关系图如下：

![](images/entryprototypeextend.png)






