# 单体内置对象

> EMCA-262对内置对象的定义是：由ECMAScript实现提供的、不依赖于宿主环境的对象，这些对象在ECMAScript程序执行之前就已经存在了。***开发人员不必显式地实例化内置对象，因为他们在执行前就已经存在了***。

主要的内置对象有：
+ Object
+ Array
+ String
+ Boolean
+ Number
+ Date
+ RegExp
+ Global
+ Math

##1. Global对象

> Global对象是ECMAScript中最特别的一个对象，不管从任何角度来说都是不存在这个对象的。ECMAScript
中把Global对象在某种意义上市作为一个终极的“兜底儿对象”来定义的。换句话说，***不属于任何其他对象
的属性和方法，最终都是属于它的属性和方法***

诸如之前所见函数：
+ isNaN
+ isFinite
+ parseInt
+ parseFloat

##1.1 URI编码方法

> 对URI（Uniform Resource Identifiers，通用资源标识符）进行编码，以便发送给浏览器。有效的URI中不能包含某些特殊字符（空格等），它们用特殊的UTF-8编码替换所有无效的字符，从而让浏览器能够接受和理解。

常见4个URI编码方法：
+ encodeURI 用于整个URI进行编码，不会对本身属于URI的特殊字符进行编码（例如：**冒号、正斜杠、问号和井字号**等），,返回新的编码字符串。
+ encodeURIComponent 主要是用于对URI中的某一段进行编码，它会对发现的任何非标准（**所有非字母、数字字符**）的字符进行编码，返回新的编码字符串。
+ decodeURI 用于对整个URI字符进行解码，与encodeURI相应对，解码要求规则一致,返回新的解码字符串。
+ decodeURIComponent 用于对URI中的某一部分字符进行解码，与encodeURIComponent相对应，解码要求规则一致，返回新的解码字符串。

```javascript
var uri = "http://mg.yitb.com/orders/index order#setting?ordertype=0";
// "http://mg.yitb.com/orders/index%20order#setting?ordertype=0"
var encodeuri = encodeURI(uri);
console.log(encodeuri); 

// "http%3A%2F%2Fmg.yitb.com%2Forders%2Findex%20order%23setting%3Fordertype%3D0"
var encodeComponentUri = encodeURIComponent(uri);
console.log(encodeURIComponent(uri))

// 解码
console.log(decodeURIComponent(encodeComponentUri));
console.log(dencodeURI(encodeuri));
```

##1.2 eval()方法

> ECMAScript语言中最强大的一个方法：eval()，它就像一个完整的ECMAScript解析器，它只接受一个参数，即要执行的ECMAScript（javascipt）字符串。

```javascript 
eval("console.log('hi')");

var msg = "hello world";
eval("console.log(msg)");

eval("function sayHi(){console.log("hello");}");
sayHi();
```

***当解析器发现代码中调用eval()方法时，它会将传入的参数当做实际的ECMAScript语句来解析，然后把执行结果插入到原位置。通过eval（）执行的代码被认为是包含该次调用的执行环境的一部分，具有与该执行环境相同的作用域链。即：可以引用执行环境中定义的变量***

> 在eval()中创建的任何变量或函数都不会被提升，因为在解析代码的时候，他们被包含在一个字符串中；他们只在eval()执行的时候创建。

```javascript
eval("var msg = 'hello world'");
console.log(msg);
```

***严格模式下，在外部访问不到eval()中创建的任何变量或函数，因此前面两个例子都会导致错误；同样，在严格模式下，为eval赋值也会导致错误：***

```javascript
'use strict'
eval = "hi";        // causes error
```

##1.3 Global对象的属性

> Global 对象还包含一些属性：

|属性       |说明         |
|-----------|-------------|
|undefined  |特殊值undefined   |
|NaN        |特殊值NaN         |
|Infinity   |特殊值Infintiy    |
|Object     |构造函数Object          |
|Array      |构造函数Array          |
|Function   |构造函数Function          |
|Boolean    |构造函数Boolean          |
|String     |构造函数String          |
|Number     |构造函数Number          |
|Date       |构造函数Date          |
|RegExp     |构造函数RegExp          |
|Error      |构造函数Error          |
|EvalError  |构造函数EvalError          |
|RangeError |构造函数RangeError          |
|ReferenceError   |构造函数ReferenceError          |
|SyntaxError      |构造函数SyntaxError          |
|TypeError        |构造函数TypeError          |
|URIError         |构造函数URIError          |

***ECMAScript5明确禁止给undifined、NaN和Infinity赋值，这样做即使在非严格模式下也会导致错误***


