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


##1. Node类型

> DOM1 级定义了一个 Node 接口，该接口将由 DOM 中的所有节点类型实现。这个 Node 接口在JavaScript 中是作为 Node 类型实现的；JavaScript 中的所有节点类型都继承自 Node 类型，因此所有节点类型都共享着相同的基本属性和方法


	每个节点都有一个 nodeType 属性，用于表明节点的类型
+      Node.ELEMENT_NODE(1)；
+  Node.ATTRIBUTE_NODE(2)；
+  Node.TEXT_NODE(3)；
+  Node.CDATA_SECTION_NODE(4)；
+  Node.ENTITY_REFERENCE_NODE(5)；
+  Node.ENTITY_NODE(6)；
+  Node.PROCESSING_INSTRUCTION_NODE(7)；
+  Node.COMMENT_NODE(8)；
+  Node.DOCUMENT_NODE(9)；
+  Node.DOCUMENT_TYPE_NODE(10)；
+  Node.DOCUMENT_FRAGMENT_NODE(11)；
+  Node.NOTATION_NODE(12)
**IE 没有公开 Node 类型的构造函数，不存在上述常亮，因此直接使用常亮IE中会报错**



