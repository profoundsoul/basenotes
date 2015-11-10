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

可以将以上的三个步骤想象成是执行了一下ECMAScript代码。
```javascript
var s1 = "some text";
var tempStr = new String(s1);
var s2 = tempStr.substring(2);
tempStr= null;
```

