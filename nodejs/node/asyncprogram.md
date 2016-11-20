# 异步编程

## 函数式编程

#### 高阶函数
> 是将函数作为参数或将函数作为返回值的函数

```javascript
var arr = [];
arr.map(x=>x);  //Array.prototype.map就是高阶函数
```

ECMAScript5中新增的some(),any(),forEach(),reduce(),filter,map(),find()等都是高阶函数。

#### 偏函数

> 通过已经内置部分变量或参数的函数所创建的函数，生成偏函数的创建者一定是高阶函数，此外一定会存在脚本闭包。
> 

```javascript
var toString = Object.prototype.toString;
function isType(type){
    return function(obj){
        return toString.call(obj) === '[object '+type+']';
    };
}

var isString = isType('String');    //偏函数
var isFunction = isType('Function');//偏函数

```

偏函数的应用十分常见，例如underscore中的after等多数函数也是偏

```javascript
_.after = function(times, func){
    if(times<=0)return func();
    return function(){
        if(--times <=0){
            return func.apply(this, arguments);
        }
    }
}
```

## 异步编程优势与难点

#### 优势

+ I/O操作性能出色
+ 充分使用I/O操作与CPU计算并行的能力

建议：cpu的耗用不能超过10ms，不超过建议使用process.nextTick，一旦超过建议使用setImmediate之类的进行处理

#### 难点

+ 异常处理
    - try^catch捕获方式发生变化，无法直接捕获异步调用函数
    - 必须执行调用者传入的回调函数
    - 正确传递回异常供调用者判断
    - 错误优先的回调函数（***常规处理原则***)
    - 约定：传递错误和数据，第一个参数必须为错误对象，回调优先处理异常情况
+ 函数嵌套太深
    - 异步回调到处都是，难免造成嵌套层数很深的情况
+ 阻塞代码
    - 无法阻塞代码，无sleep(1000)之类函数
    - 一定使用while(true)类似代码阻塞，会导致破坏事件循环的调度
    - 由于Node是单线程的原因，CPU资源全都会为这段代码服务，导致其它任何请求都不会得到响应
+ 多线程编程，利用多CPU
    - 在浏览器中Javascript执行和UI渲染共用一个线程
    - 浏览器中提供Web Worker
    - Node中提供child_process 基础API
    - cluster模块是更深层次的应用
+ 异步转同步难
    - 借助第三方库进行处理

## 异步编程解决方案

+ 事件发布/订阅模式
+ Promise/Deferred模式
+ 流程控制库模式

