# 引用类型 

## Object类型

> Object类型是日常引用类型中最常用的类型。创建Object对象的方法有两种
+ 使用new对象创建对象
+ 直接使用字面量表示法创建

```javascript
var obj = new Object();
var obj2={aa:test};
```

> Object常用的访问属性方法
+ 使用.号直接访问，访问的字符串不能包括空格
+ 使用[]加字符串访问，允许属性名称加空格


```javascript
var obj = {};
obj.name = "linq";
obj["i q"] = 11;
```

## Array类型

> ECMAScript中常用的类型，存储有序列表数据的数组，但与一般面向对象数组不同：
+ 每一项数据类型动态化，即：每一项的数据类型因存储数据的类型而定。
+ 数组的大小动态变化，即：随的数据的增加而自动增长

```javascript
var arr = Array(1);
arr.push("tt");
arr.push("test");
arr.push(true);       //测试arr的length为3
```

> 实例化数据Array对象常见的有两种方式：
* new实例化，允许传入多个参数依次作为数组项存入数组。若传入一个参数且为数字，会当成数组初始长度参数。
* 字面量实例化（[]）。

```javascript
var arr1 = new Array();
var arr2 = new Array(3);
var arr3 = new Array("tt","qqq", "ddd");
var arr4 = ["addddd"];
var arr5 = Array(10);
var arr6 = Array(10, 23,35,3);
```

##注意：数组实例化也可以省略new。和带New用法含义一模一样##


