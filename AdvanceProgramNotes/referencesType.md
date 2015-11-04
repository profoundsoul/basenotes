# 引用类型 

## Object类型

> Object类型是日常引用类型中最常用的类型。创建Object对象的方法有两种
+ 使用var obj = new Object();
+ 直接使用字面量表示法var obj2={aa:test};


> Object常用的访问属性方法
+ 使用.号直接访问，访问的字符串不能包括空格
+ 使用[]加字符串访问，允许属性名称加空格


```javascript
var obj = {};
obj.name = "linq";
obj["i q"] = 11;
```




