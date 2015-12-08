# Variable Attention

## 全局变量

> 由于Javascript有两个特征，不自觉的创建出全局变量出乎意料的容易。

***1. 你可不需要申明的使用变量，这样创建出来的变量就是全局变量***

```javascript
function sum(a,b){
  result = a + b;       //自动创建全局变量result----window.result可以访问
  return result;
}
```

***2. 使用任务链进行部分var声明变量，根本原因一般是由于任务链赋值是由右向左导致的***

```javascript
function test(){
  var a = b = 11;     //此时b为全局变量
  //由于任务链赋值是由右向左，等同于下面代码
  var a = (b= 11);
  
  //推荐使用下面的定义方法：
  var a,b;
  a = b = 11;
}

```

***3. 忘记Var创建全局变量的副作用***
> 隐式全局变量和明确定义的全局变量还是有些微小的区别的，可以通过delete操作符来识别
+ 隐式全局变量可以用delete删除
+ 显式全局变狼不能用delete删除

```javascript
var global_var = 11;
global_novar = 12;

delete global_var ; //删除失效

delete global_novar ;//删除成功

```
