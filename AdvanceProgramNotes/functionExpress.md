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


##1. 递归

> 递归函数是在一个函数通过调用自身的情况下构成的。

```javascript 
function factorial(num){
  if(num == 1){
    return 1;
  }
  return n * factorial(num-1);
}

//若换成下面调用方式，会报错
var anotherFn = factorial;
factorial = null;
anotherF();//报错
```

> 在非严格模式下，调用解决此错误处理方案：使用argument.callee

```javascript
function factorial(num){
  if(num == 1){
    return 1;
  }
  return num * argument.callee(num-1);
}

```

***严格模式下，argument.callee会报错误***

> 严格模式处理方案：使用**立即执行函数**来保证函数的作用域

```javascript
var factorial = (function f(num){
  if(num ==1){
    return 1;
  }
  return num * f(num -1)
})();

```

***推荐使用方式***





