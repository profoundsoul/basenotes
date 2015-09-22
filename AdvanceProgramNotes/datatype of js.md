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

### 1. Undefined类型

> Undefined类型只有一个值，即特殊值undefined。在使用var声明变量但未对其加以初始化时，这个变量的值就是undefined。

例如：

```javascript
var message;
console.log(message == undefined);    // true
```

> 对于未初始化的变量执行typeof操作符会返回undefined值，而对于未声明的变量执行typeof操作符同样也会返回undefined值。

例子：
```javascript
var message;
console.log(typeof message);	// "undefined"
console.log(typeof age);		// "undefined"
```

### 2. Null类型

> Null类型是第二个只有一个值得数据类型，这个特殊的值是null。从逻辑角度来看，null值表示一个空对象指针，这也正是**typeof操作符检测null值时会返回"object"的原因。

例如：
``` javascript
var car = null;
console.log(typeof car);	// "object"
```
> 实际上，undefined值是派生自null的值，因此ECMA-262规定对它们的相等性测试要返回true。

例如：
``` javascript
console.log(undefined == null);		// true
```

### 3. Boolean类型

> 是ECMAScript中使用的最多的一种类型，该类型只有两个字面值：true和false。值得注意的是：区分大小写（True和False不是Boolean类型），然而ECMAScript中所有类型都这两个Boolean等价的值。

例如：
``` javascript
var message = "hello world!";
var msgAsBool = Boolean(message);
```

**各种数据类型与Boolean对应的转换规则**：

|数据类型          |转换为true的值             |转换为false的值        |
| ------------  | :----------------------: | :------------------: |
|Boolean          | true                     | false                |
|String           | 任何非空字符串            | ""（空字符串）        |
|Number           | 任何非零数字值（包括无穷大）|0和NaN                |
|Object           | 任何对象                  |null                  |
|undefined        | 无							|undefined			|

> 这些转换规则对于理解流程控制语句（例如if语句）自动执行相应的Boolean转换非常重要。

例如：
``` javascrip
var msg = "hello world!";
if(msg){
	console.log('value is true');
}
```                             
> *上面这个示例存在自动执行Boolean转换，因此确切地知道流程控制语句中使用的是什么变量只管重要*。

### 4. Number类型

> Number类型是EMCAScript最关注的类型；使用IEEE754格式来表示整数和浮点型数值。为了支持各种数值类型，ECMA-262定义了不同的数值字面量格式。

* 十进制字面量。
```javascript
	var intNum = 55;  //整数
```

* 八进制字面量，第一位必须是**0**，然后是八进制数字序列（0~7）。如果字面值数值超出范围，那么前面的零将被忽略，后面数值当成十进制解析。
```javascript
	var actalNum = 070;   //八进制的56
	var actalNum2 = 079;  //十进制79
	var actalNum3 = 08;   //十进制8
```
***八进制字面量在严格模式下是无效的；引擎抛出错误。***

* 十六进制字面量，前两位必须是0x，后面任何十六进制数字（0~9及A~F）。其中字母A~F可以大写，也可以小写。
```javascript
var hexNum1 =0xA;    //十六进制的10
var hexNum2 =0x1f;   //十六进制的31
```
***进行算术计算时，所有八进制和十六进制表示的数值都将转换成十进制数值。***

#### 1. 浮点数值

> 所谓浮点数值，就是该数值中必须包含一个小数点，小数点后面必须要有一位数字。但小数点前面可以没有整数___不推荐这种写法___。

例如：
```javascript
	var floatNum1 = 1.1;
	var floatNum2 = 0.1;
	var floatNum3 = .1      //有效，但不推荐
```

> 由于保存浮点数值需要的内存空间是保存整数的*两倍*，因此ECMAScript会不失时机的将浮点数值转换为整数值。
* 小数点后面没有跟任何数字--转换为整数保存
* 如果浮点型表示的就是一个整数，该值也会被转换为整数

```javascript
	var f1 = 1.;	//整数1
	var f2 = 1.0;	//整数1
```










