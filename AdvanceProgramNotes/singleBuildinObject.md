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




