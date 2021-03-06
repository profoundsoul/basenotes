
DOM（文档对象模型）是针对 HTML 和 XML 文档的一个 API（应用程序编程接口）

DOM 描绘了一个层次化的节点树，允许开发人员添加、移除和修改页面的某一部分。 DOM 脱胎于Netscape 及微软公司创始的 DHTML（动态 HTML），但现在它已经成为表现和操作页面标记的真正的跨平台、语言中立的方式。
     
关于元素位置、尺寸可参考下面文章:

<http://www.jianshu.com/p/187c0145248c>

<http://www.jianshu.com/p/92611d719a93>



# DOM节点层次

> DOM 可以将任何 HTML 或 XML 文档描绘成一个由多层节点构成的结构。
+ 节点分为几种不同的类型，每种类型分别表示文档中不同的信息及（或）标记。
+ 每个节点都拥有各自的特点、数据和方法
+ 其他节点存在某种关系，构成节点层次关系（树形节点）



```
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" /> 
	<title>无标题</title>
</head>
<body>
</body>
</html>

```

可以将这个简单的 HTML 文档表示为一个层次结构，解析：
+ 文档节点是每个文档的根节点，即：可以把这个HTML文件看成文档节点
+ 文档元素：文档节点的子元素，即：html节点

***在 HTML 页面中，文档元素始终都是<html>元素。在 XML 中，没有预定义的元素，因此任何元素都可能成为文档元素***


> 每一段标记都可以通过树中的一个节点来表示：
+ 元素节点：HTML元素
+ 特性节点：特性
+ 文档类型节点：文档类型
+ 注释节点：注释
+ …………………………………………………………，总共12中节点类型