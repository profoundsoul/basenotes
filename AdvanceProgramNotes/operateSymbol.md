# 操作符

## 加号(+)

### 两数值相加
>常用，但操作符有特殊规则（数值相加）

+ 有任何一个是NaN，返回NaN
+ 两个Infinite相加，返回Infinite
+ 两个-Infinite相加，返回-Infinite
+ Infinite与-Infinite相加，返回NaN
+ 两个+0相加，返回+0
+ 两个-0相加，返回-0
+ +0与-0相加，返回+0

### 至少有一个字符串相加

> 在操作符有一个是字符串时，特殊处理+号

+ 如果有一个是字符串，将非字符串转换为字符串进行字符串拼接
+ 如果两个都是字符串，直接将字符串拼接

### 其它

> 其它组合（undefined、null、boolean、object）

+ 按照组合规则，右侧如果是Object（包含function但非null），会将对象toString，按照string相加的方式去处理
+ 如果右侧是undefined、null、boolean，所有变量自动转换为number进行相加.转换规则Number

```javascript
undefined + {}       //undefined[object Object]
false + function(){} //falsefunction (){}
{} + undefined       //NaN
{} + false           //0,硬性规定忽略左侧对象当成0来处理
{} + null            //0,
null + false         //false
false + undefined    //NaN
```

## 减号

>特殊规则：

+ 如果存在NaN，返回NaN
+ Infinite或-Infinite相减，返回NaN
+ Infinite减去-Infinite，返回Infinite
+ -Infinite减去Infinite，返回-Infinite
+ 如果有任何一个为undefined、null、boolean、string类型都自动转换为Number类型进行运算
+ 如果有个操作数是对象，优先调用valueOf，在考虑toString

## 乘、除、取模

>特殊规则：

+ 如果存在NaN，返回NaN
+ 如果有非数字，将调用Number进行转换为数值进行操作


