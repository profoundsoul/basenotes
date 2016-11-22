# JavaScript执行环境 + 变量对象 + 作用域链 + 闭包

<http://www.cnblogs.com/no-particular/archive/2013/01/31/2887293.html>

> 《深入理解JavaScript系列》系列技术文章整理收藏：
+ <http://www.douban.com/group/topic/76381218/>

## 闭包

一旦形成闭包后，会导致整个执行上下文的变量对象均存活下来，尤其是函数，DOM对象等，容易造成“吃内存”现象，例如：

```javascript
$(function(){
    var arr = new Array(10000);
    var mainEle = $('#main');
    mainEle.on('click', function(){
        console.log(mainEle.attr('data-main'));
    });

    function getValue(dom){
        return 'test';
    }
});

```

上述代码，会造成mainEle元素形成一个闭包，长久不能得到释放。因此匿名函数function的变量对象均会存活下来（包含getValue函数、arr数组等），仅仅是除了mainEle外，其它对象都不能被外部访问。但依然会造成整个变量对象【活动对象】无法内存无法释。我们称其为变相形式的内存泄露。

### 解除引用

> 数据一旦不使用了，将其引用设置为null的方式，成为引用解除。所有变量均解除引用时，对象会被认为“离开环境”被垃圾回收器回收

```javascript
$(function(){
    var arr = new Array(10000);
    mainEle.on('click', function(ee){
        var target = $(ee.currentTarget);
        console.log(target.attr('data-main'));
        target = null;
    });

    function getValue(dom){
        return 'test';
    }
    arr = null;
    mainEle = null;
});
```

***解除引用可以避免很多内存泄露问题，但是如果是闭包导致的“吃”内存问题，解除引用很难从根本上解决***

## 垃圾回收


### 标记和清除算法（Mark-Sweep）

> 对global对象进行循环递归标记存活对象，未必标记对象进行垃圾回收.

主体上分两阶段：
+ 从根节点标记所有被引用的对象
+ 遍历整个堆，把未被标记的对象清除

弊端：
+ 整个应用程序停顿
+ 产生内存碎片

### 引用计数（Reference Counting）

原理：
+ 对此对象有一个引用，就增加一个计数；删除一个引用就减少一个计数
+ 垃圾回收时，只收集计数为0的对象。

弊端：
+ 无法处理循环引用的问题

### Scavenge复制（Coping）

原理：
+ 每次分配内存时，把空间划分为两个相等区域，每次只使用一个区域
+ 垃圾回收时，遍历活动对象复制到另一个区域，将两个区域角色对调

优点：
+ 不出现内存碎片
+ copy成本比较低

弊端：
+ 需要两倍内存空间

### 标记-整理（mark-compact）

原理：
+ 从根节点开始标记被引用的对象
+ 遍历整个堆，清除未标记对象并将已标记对象“压缩”到堆的其中一块，按照顺序排放。

优势（结合标记-清除与复制算法）：
+ 避免内存碎片
+ 空间问题

### 增量收集

原理：
+ 在应用进行的时候，进行垃圾回收


### 分代回收（Generational Collection）

> 基于对象的生命周期分析后的垃圾回收机制，吧对象年轻代、老年代和持久代的对象使用不同的回收算法。J2SE1.2/V8均使用算法

### GC分类

> GC有两种类型：Scavenge GC和Full GC。 

## 内存泄露

[四类Javascript内存泄露如何避免](http://jinlong.github.io/2016/05/01/4-Types-of-Memory-Leaks-in-JavaScript-and-How-to-Get-Rid-Of-Them/)


