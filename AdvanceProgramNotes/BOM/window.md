# window对象

> BOM的核心对象是window，它表示浏览器的一个实例。在浏览器中，window对象有双重角色：
+ 通过JavaScript访问浏览器窗口的一个接口
+ 又是ECMAScript规定的Global对象。这意味着在网页中定义的任何一个对象、变量和函数，都以window作为其Global对象，因此有权访问parseInt等全局方法。

##1. 全局作用域

> 由于window对象同时扮演的ECMAScript中的Global对象的角色，因此所有在全局作用域中声明的变量、函数都会变成window对象的属性和方法。例如：

```javascript
var age = 29;
function sayAge(){
	console.log(this.age);
}
console.log(window.age);		//29
sayAge();				//29
window.sayAge();			//29

```

我们在全局作用域中定义了一个变量age和一个函数sayAge()，他们都自动归在了window对象的名下，于是我们可以通过window访问变量age和函数sayAge。由于sayAge存在于全局作用域中，因此this.age中this相当于window对象。

> 全局变量与全局属性的最基本区别：全局变量不能通过delete操作符删除，而直接在window中定义的属性可以。

```javascript
var age = 29;
window.color = 'red';

// 在IE<9 时抛出错误，在其它所有的浏览器中都返回了false
delete window.age;

// 在IE<9 时抛出错误，在其它所有的浏览器中都返回了true
delete window.color;

console.log(window.age);	//29
console.log(window.color);	//undefined

```

##2. 窗口关系及框架

> 如果页面中包含框架，则每个框架都拥有自己的window对象，并且保存在frames集合中。在frames集合中，可以通过数值索引（从0开始，从左到右，从上到下）或者框架名称来访问相应的window对象。

```
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" /> 
	<title>无标题</title>
</head>
<frameset rows='160,*' name="topframe">
	<frame src="frame.html"></frame>
	<frameset cols="50%,50%">
		<frame src='anotherframe.html'></frame>
		<frame src='yetanotherframe.html'></frame>
	</frameset>
</frameset>
</html>

```

上述例子中，可以通过window.frames[0]或者window.frames['topframe']来引用上方的框架。不过您最好使用top.frames来访问最外层的框架。

> 对于window框架相关术语，有几个特殊的对象：
+ top 始终指向最外层的window对象
+ seft 始终指向当前的window对象
+ parent 始终指向当前window对象的父window对象。

