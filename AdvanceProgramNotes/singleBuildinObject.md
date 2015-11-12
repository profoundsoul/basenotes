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

>
