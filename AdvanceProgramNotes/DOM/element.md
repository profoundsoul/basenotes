# Element 类型

> Element 类型用于表现 XML 或 HTML 元素，提供了对元素标签名、子节点及特性的访问。 Element 节点具有以下特征：
+ nodeType 的值为1
+ nodeName的值为元素的标签名
+ nodeValue的值为null
+ parentNode 可能是Element或Document
+ 其子节点可能是Element、Text、Comment、ProcessingInstruction、CDATASection或EntityReference


#### tagName与nodeName

```javascript
var div = document.getElementById("myDiv");
alert(div.tagName); //"DIV"
alert(div.tagName == div.nodeName); //true

```

**在 HTML 中，标签名始终都以全部大写表示；而在 XML（有时候也包括 XHTML）中，标签名则始终会与源代码中的保持一致**


##1.  HTML元素

> 