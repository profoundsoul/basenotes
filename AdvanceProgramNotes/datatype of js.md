## javascript 数据类型
> ECMAScript中有5种简单的数据类型（基础数据类型）和一种复杂数据数据类型：
  * Undefined
  * Null
  * Boolean
  * Number
  * String 
  * Object

### typeof检测数据类型
> 鉴于ECMAScript 是松散类型的，因此需要一种手段来检测给定变量的数据类型--typeof就是负责提供这方面信息的*操作符*。对一个值使用typeof操作符可能返回下列某个字符串：

  * "undefined"----未定义
  * "boolean"------布尔值
  * "number"-------数值
  * "string"-------字符串
  * "object"-------对象
  * "function"-----函数

例子：
```javascript
var message = 'some string';
alert(typeof message);      //string
alert(typeof(message));		//string
alert(typeof 95);			//number
```

1. Undefined类型
> Undefined类型只有一个值，即特殊值undefined。在使用var声明变量但未对其加以初始化时，这个变量的值就是undefined，例如：
```javascript
var message;
console.log(message == undefined);    // true
```

