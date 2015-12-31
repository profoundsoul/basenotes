# 高性能JavaScript DOM编程以及重排与重绘

本篇主要源自于：<http://developer.51cto.com/art/201508/488053.htm>

附加html页面的渲染过程：<http://www.cnblogs.com/yuezk/archive/2013/01/11/2855698.html>

> 我们知道，DOM是用于操作XML 和HTML文档的应用程序接口，用脚本进行DOM操作的代价很昂贵。有个贴切的比喻，把DOM和JavaScript（这里指ECMScript）各自想 象为一个岛屿，它们之间用收费桥梁连接，ECMAScript每次访问DOM，都要途径这座桥，并交纳“过桥费”,访问DOM的次数越多，费用也就越高。 因此，推荐的做法是尽量减少过桥的次数，努力待在ECMAScript岛上。我们不可能不用DOM的接口，那么，怎样才能提高程序的效率？

## Dom编程优化

###1. DOM访问与修改

> 访问DOM元素是有代价的（“过桥费”你懂的），修改元素代价更是昂贵，因为它会导致浏览器重新计算页面的几何变化（重排和重绘）。

当然最坏的情况是在循环中访问或者修改元素，看下面两段代码：

```javascript
var times = 15000;

// code1
console.time(1);
for(var i = 0; i < times; i++) {
  document.getElementById('myDiv1').innerHTML += 'a';
}
console.timeEnd(1);

// code2
console.time(2);
var str = '';
for(var i = 0; i < times; i++) {
  str += 'a';
}
document.getElementById('myDiv2').innerHTML = str;
console.timeEnd(2);

```

***结果第一次运行的时间居然是第二次的千倍！(chrome 版本 44.0.2403.130 m)***

1: 2846.700ms
2: 1.046ms

解析：

  第一段代码的问题在于，每次循环迭代，该元素都会被访问两次：一次读取innerHTML的值，另一次重写它，也就是说，每次循环都在过桥（重排和重绘将在下一篇讲解）！结果充分表明，访问DOM的次数越多，代码的运行速度越慢。

总结：

***能减少DOM访问的次数则尽量减少，尽量留在ECMAScript这端处理。***

###2. HTML集合 & 遍历DOM

> 操作DOM另一个耗能点就是遍历DOM，一般我们会收集一个HTML集合，比如用getElementsByTagName()，或者用document.links等，我想大家对此都不陌生。收集的结果是一个类似数组的集合，它处于一种**“实时状态”**实时存在。
+ 当底层文档对象更新时，它也会自动更新
+ 遍历、访问属性方法操作是实时查询Dom结构
+ 集合使用时自动变化


```
<body>
  <ul id='fruit'>
    <li> apple </li>
    <li> orange </li>
    <li> banana </li>
  </ul>
</body>
```

```javascript
var lis = document.getElementsByTagName('li'); 
var peach = document.createElement('li'); 
peach.innerHTML = 'peach'; 
document.getElementById('fruit').appendChild(peach); 
console.log(lis.length); // 4
```

而这正是低效之源！

很简单，跟数组的优化操作一样，缓存个length变量就ok了（***读取一个集合的length比读取一个普通数组的lengh要慢很多，因为每次都要查询***）：

```javascript

console.time(0);
var lis0 = document.getElementsByTagName('li');
var str0 = '';
for(var i = 0; i < lis0.length; i++) {
  str0 += lis0[i].innerHTML;
}
console.timeEnd(0);


console.time(1);
var lis1 = document.getElementsByTagName('li');
var str1 = '';
for(var i = 0, len = lis1.length; i < len; i++) {
  str1 += lis1[i].innerHTML;
}
console.timeEnd(1);

```

我们看看性能提升能有多少？

0: 0.974ms

1: 0.664ms

而《高性能JavaScript》提出了另一个优化策略，它指出，“由于遍历数组比遍历集合快，因此如果先将集合元素拷贝到数组中，那么访问它的属性会更快”


###3. querySelector()和querySelectorAll()

> 前者返回一个第一个元素（注意，**它们的返回值不像HTML集合一样会动态变化**），后者返回匹配的数组。

其实并不是所有时候它的性能都优于前者的HTML集合遍历：

```javascript
console.time(1);
var lis1 = document.getElementsByTagName('li');
console.timeEnd(1);

console.time(2);
var lis2 = document.querySelectorAll('li');
console.timeEnd(2);

// 1: 0.038ms
// 2: 3.957ms
```

***它是类似CSS的选择方法，所以在做组合选择的时候，效率会提升，又方便***。比如做如下的组合查询：

```javascript

var elements = document.querySelectorAll('#menu a');
var elements = document.querySelectorAll('div.warning, div.notice');

```



## 重排和重绘

> 
