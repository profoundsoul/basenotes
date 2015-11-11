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

## String类型

> String类型是字符串的对象包装类型。

***String对象的方法也可以在所有的基本字符串值中访问到。其中继承的valueOf（）、toLocaleString（）和toString（）方法，都返回对象所表示的基本字符串值***

```javascript
var stringObj = new String('hello World');
console.log(stringObj.toString());
console.log(stringObj.valueOf());
```

> length属性, String类型的每一个实例都有一个length属性，表示字符串中包含多个字符。***即使字符串中包含双字节字符（不是占一个字节的ASCII字符），每个字符也仍然算一个字符***。

```javascript
var s = new  String('sdsd多岁的ff');
console.log(s.length);              //9
```


###1. 字符方法

> 用于访问字符串中特定字符的方法：
+ charAt(index) 以单字符字符串的形式返回给定位置的那个字符
+ charCodeAt(index) 返回给定位置的那个字符的字符编码

```javascript
var stringValue = "teacher";
console.log(stringValue.charAt(1));     //"t",注意是单字符串值
console.log(stringValue.charCodeAt(1)); //"101",字符编码
```

***ECMAScript5中还定义了另一个访问个别字符串的方法。在支持此方法的浏览器中，可以使用括号加数字索引来访问字符串中的特定字符，目前支持的浏览器IE8+以及其他浏览器***

```javascript
var str = "technology";
console.log(str[1]);        // "e"
```

###2. 字符串操作方法

> 常用的字符串操作方法
+ concat(str,...) 将一个字符串或多个字符串拼接起来，返回拼接得到的新字符串。与实用**+**相同。
+ slice(startIdx, endIdx) 传入一个或两个参数, 返回操作字符串的一个子字符串。
+ substr(startIdx, length) 传入一个或两个参数，返回操作字符串的一个子字符串。
+ substring(startIdx, endIdx) 传入一个或两个参数，返回操作字符串的一个子字符串。

```javascript
var str = "hello world";
console.log(str.slice(-3));     // rld
console.log(str.substring(-3)); //hello world
console.log(str.substr(-3));    //rld

console.log(str.slice(3, -4));  //lo w
console.log(str.substring(3, -4));  //hel
console.log(str.substr(3, -4));     //""
```

区别：
+ slice和substr传入第一个参数传入负值，会自动加上length * N + index来使用。而substring传入负值直接转换为0使用。
+ 当第二个参数为负值时，slice方法会自动加上length * N + index; substr和substring都会自动转换为0。而substring会自动从小的位置开始；substr则不会，直接返回空字符串。

###3. 字符串位置方法

> 查找子字符串的两个常用方法：
+ indexOf(str, srchIdx)
+ lastIndexOf(str, srchIdx)













