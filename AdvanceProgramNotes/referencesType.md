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

> 数组的访问特点和length妙用
* 数组使用[]访问，一般与正常语言访问一致。但若index超出length时，会自动扩充数组大小并返回undefined值
* length属性可读写。修改length的值可以扩充/缩减数组长度。

```javascript
var arr = new Array("red", "green", "blue");  
arr[5]="ttt";             //自动扩充长度为6,第4、5项内容为undefined
arr.length = 3;           //删除数组第三项后的内容，并将长度变为3
arr[arr.length] = "test"; //自动增加下一项，相当于push
```

### 1. 检测类型

> ECMAScript3中确定某个对象是不是一个数组就成为经典问题。对于一个网页或全局对象而言，直接使用instanceOf操作符即可。但如果存在两个不同的全局环境时，会存在两个不同的Array构造函数，判断会失效。
为了解决此问题，ECMASCript5中新增了Array.isArray方法。但也只对IE9+、FF4+有效。

```javascript
    // detection Array,default Array.isArray
    window.isArray = Array.isArray || function(obj){
        Object.prototype.toString.call(obj) === '[object Array]';
    };

    console.log(isArray([]));
```

### 2. 转换方法

+ toString  默认会直接返回数组采用逗号分隔字符串
+ valueOf   默认返回数组本身
+ toLocaleString 

###3. 栈操作


