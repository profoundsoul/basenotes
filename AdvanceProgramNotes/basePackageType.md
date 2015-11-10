# 基本包装类型

> 为了便于操作基本类型值，ECMAScript还提供了3个特殊的引用类型：Boolean、Number、String。不仅具有其他引用类型的特性，同时也具有与各自的基本类型响应的特殊行为。

***实际上，每当读取一个基本类型的值的时候，后台就会创建一个对应的基本包装类型的对象，从而让我们能够调用一些方法来操作这些数据***

```javascript
var s1 = "some text";       //基本类型值
var s2 = s1.substring(2);   //自动创建String实例，调用substring方法处理基本类型值
```

*处理基本类型值真实处理过程*
+ 创建String（基本包装类型）的一个实例
+ 在实例上调用指定的方法
+ 销毁这个实例

可以将以上的三个步骤想象成是执行了一段ECMAScript代码。
```javascript
var s1 = "some text";
var tempStr = new String(s1);
var s2 = tempStr.substring(2);
tempStr= null;
```

***以上的三个操作步骤也分别适用于Boolean和Number类型对应的布尔值和数字值***

--------------------------------------------------------------

***引用类型和基本包装类型的最主要区别：对象的生存期***
> 使用new操作符创建的引用类型的实例，在执行流离开当前作用域之前都一直保存在内存中。而自动创建的基本包装类型的对象，则只存在于一行代码的执行瞬间，然后立即销毁。***这意味的我们不能再运行时为基本类型值添加属性和方法***。

```javascript
var s1 = "some text";
s1.color = "red";
console.log(s1.color);      //undefined
```

> 对于基本包装类型调用typeof会返回"object"，***特殊的Object构造函数传入基本类型值会自动转换为基本包装类型***

```javascript
var obj = new Object('some text');
console.log(obj instanceof String);     //true
var obj2 = new Object(123);
console.log(obj2 instanceof Number);    //true
```

> 注意：***使用new调用基本包装类型的构造函数，与直接调用同名的转型函数是不一样的***

```javascript
var value = "32";
var number = Number(value);
console.log(typeof number);        //"number"

var obj = new Number(value);
console.log(typeof obj);            //"object"
```

**这个例子中,number保存的是基本类型值。而obj保存的是Number的包装类型实例**

## Boolean类型

> Boolean类型是与布尔值对应的引用类型。

```javascript
var falseObject = new Boolean(false);
var falseValue = false;

console.log(typeof falseObject);      //object
console.log(typeof falseValue);       //boolean
console.log(falseObject instanceof Boolean);      //true
console.log(falseValue instanceof Boolean);       //false
```

## Number类型

> Number是与数字值对应的引用类型。

***常见的数值包装类型的实用方法***
+ toFixed(decimalDigit) 会按照指定的小数位返回数值的字符串值表示，能够自动四舍五入处理。
+ toExponential(decimalDigit) 会按照指定的小数位返回以指数表示法的数值字符串值表示。
+ toPrecision(digit) 会按照所有数字的位数返回固定大小或指数的格式，自动截断或进位表示。

```javascript 
var num = 99.32457;

console.log(num.fixed(3));      //"99.325"
console.log(num.toExponential(2));  //"9.93e+1"
console.log(num.toPrecision(1));    //1e+2"
```

### String类型

> String类型是字符串的对象包装类型。










