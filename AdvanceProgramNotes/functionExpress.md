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

> 严格模式处理方案：使用**命名函数表达式**来保证函数的作用域

```javascript
var factorial = (function f(num){
  if(num ==1){
    return 1;
  }
  return num * f(num -1)
});

```

***推荐使用方式***

##2. 模仿块级作用域

> JavaScript中没有块级作用域的概念。这意味的在块级作用域中定义的变量，实际上是包含在非语句中创建的。

```javascript
function outPutNumber(num){
  for(var i = 0; i< num; i++){
    console.log(i);
  }
  console.log(i);//显示出Num的值来，能够正常访问
  
  var i ;           //上面已经定义，对此重复定义视而不见
  console.log(i);   //num
  
}

```
***在javaScript中，变量是定义在函数的活动对象中，因此从它有定义的开始，就可以在函数的内部随处访问它***

> 匿名函数可以用模块级作用域并避免javaScript中无块级作用所带来的问题。
+ 匿名函数常规写法：  (function(){....}())或(function (){})()

```javascript
function outPutNumber(num){
  (function(){
    for(var i =0; i< num; i++){
      console.log(i);
    }
  })();
  console.log(i);     //报错，因为i被申明在私有作用域中，执行完后立即被销毁，外面无法访问。
}



```

> 匿名函数解决变量绑定问题
+ 匿名立即执行函数
+ 匿名函数作为对象返回

```javascript

function f(){
  for(var i =0; i<10; i++){
    (function(){
      var j = i;
      setTimeout(function(){
        console.log(j);
      },10);
    })();
  }
}

function f2(){
  var callback = function(param){
    return function(){
      console.log(param);
    };
  };
  for(var i =0;i<10; i++){
    setTimeout(callback(i), 10);
  }
}

function f3(){
  for(var i =0; i<10; i++){
    setTimeout((function(){
      console.log(i);
    })(), 10);
  }
}

function f4(){
  for(var i=0; i<10; i++){
    setTimeout(outPut.bind(this, i), 10);
  }
}

function outPut(n){
    console.log(n);
}

```

> 匿名函数经常用于全局作用域中被用作外部函数，从而限制了往全局对象中添加不必要的属性和方法（过多）。通过创建私有作用域，尽量避免大型项目中全局对象中的命名冲突，也不必担心搞混乱了全局对象。

```javascript
(function(){
  var now  = new Date();
  if(now.getMonth() == 0 && now.getDate() == 1){
    console.log('today is new year!');
  }
})();

```

***这种做法可以减少闭包占用内存的问题，因为没有指向匿名函数的引用，只要函数执行完毕，就立即销毁其作用域***






