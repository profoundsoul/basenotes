# 函数表达式

> 函数表达式是JavaScript中最强大又容易令人困惑的特性。也是函数定义的两种方法之一
+ 函数申明，会有函数提升特性。即：读取作用域代码之前会先读取函数申明，以便该函数在作用域中能被正常调用，哪怕函数申明在代码调用之后。
+ 函数表达式，即时调用申明函数的作用。又称为匿名函数，通常函数属性name值为""

```javascript
var sayHi ;

if(condition){
  sayHi = function(){
    console.log('hello!');
  };
}else{
  sayHi = function(){
    console.log('World!');
  };
}

```

***若换成函数申明，上诉代码会出现各种浏览器Bug***

