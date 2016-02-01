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

>  所有 HTML 元素都由 HTMLElement 类型表示，不是直接通过这个类型，也是通过它的子类型来表示。HTMLElement 类型直接继承自 Element 并添加了一些属性，每个HTML标准特性：
+ id      元素在文档中的唯一标识符
+ title   有关元素的附加说明信息
+ dir    语言的方向,ltr和rtl
+ lang 语言代码
+ className 与元素的class属性对应，指定CSS类


```
<div id="myDiv" class="bd" title="Body text" lang="en" dir="ltr"></div>
```


```javascript

var div = document.getElementById("myDiv");
alert(div.id);                                   //"myDiv""
alert(div.className);                   //"bd"
alert(div.title);                                //"Body text"
alert(div.lang);                              //"en"
alert(div.dir);                                 //"ltr"

```

所有的HTMLElement元素表：

|  元素               |  类型                              | 
|------------------|---------------------------- |
|a                        | HTMLAnchorElement  |
|abbr                  | HTMLElement              |
|acronym           | HTMLElement              |
|address            | HTMLElement              |
|erea                   | HTMLAreaElement      |
|b                         | HTMLElement              |
|base                   |  HTMLBaseElement     |
|bdo                     |  HTMLElement              |
|big                      |  HTMLElement             |
|blockquote        |   HTMLQuoteElement  |
|body                  |   HTMLBodyElement    |
|br                       |   HTMLBRElement        |
|button                |   HTMLButtonElement  |
| caption              |    HTMLTableCaptionElement  | 
| cite                     |    HTMLElement            |
| code                  |    HTMLElement              |
| col                      |    HTMLTableColElement  |
| colgroup            |    HTMLTableColElement  |
| dd                       |     HTMLElement                |
| del                      |     HTMLModElement         |
| dfn                      |     HTMLElement                |
| div                      |     HTMLDivElement         |
| dl                         |    HTMLDListElement        |
| dt                          |   HTMLElement                 |
| em                          |   HTMLElement                 |
| fieldset                          |   HTMLFieldSetElement                 |
| form                          |   HTMLFormElement                 |
| frame                          |   HTMLFrameElement                 |
| frameset                          |   HTMLFrameSetElement                 |
| h1                          |   HTMLHeadingElement                 |
| h2                          |   HTMLHeadingElement                 |
| h3                          |   HTMLHeadingElement                 |
| h4                          |   HTMLHeadingElement                 |
| h5                          |   HTMLHeadingElement                 |
| h6                          |   HTMLHeadingElement                 |
| head                          |   HTMLHeadElement                 |
| hr                          |   HTMLHRElement                 |
| html                          |   HTMLHtmlElement                 |
| i                          |   HTMLElement                 |
| iframe                          |   HTMLIFrameElement                 |
| img                          |   HTMLImageElement                 |
| input                          |   HTMLInputElement                 |
| ins                          |   HTMLModElement                 |
| kbd                          |   HTMLElement                 |
| label                          |   HTMLLabelElement                 |
| legend                          |   HTMLLegendElement                 |
| link                          |   HTMLLinkElement                 |
| map                          |   HTMLMapElement                 |
| meta                          |   HTMLMetaElement                 |
| noframes                      |   HTMLElement                 |
| noscript                          |   HTMLElement                 |
| object                             |  HTMLObjectElement                 |
| ol                                    |   HTMLOListElement                 |
| optgroup                         |   HTMLOptGroupElement                 |
| option                             |  HTMLOptionElement                |
| p                                     |   HTMLParagraphElement                |
| param                          |   HTMLParamElement                 |
| pre                              |   HTMLPreElement                 |
| q                                   |   HTMLQuoteElement                 |
| s                                   |   HTMLElement                 |
| samp                          |   HTMLElement                 |
| script                          |   HTMLScriptElement                 |
| select                          |   HTMLSelectElement                 |
| small                          |   HTMLElement                 |
| span                          |   HTMLElement                 |
| strong                          |   HTMLElement                 |
| style                          |   HTMLStyleElement                 |
| sub                          |   HTMLElement                 |
| sup                          |   HTMLElement                 |
| table                          |   HTMLTableElement                 |
| tbody                          |   HTMLTableSectionElement                 |
| td                          |   HTMLTableCellElement                 |
| texterea                          |   HTMLTextAreaElement                 |
| tfoot                          |   HTMLTableSectionElement                 |
| th                          |   HTMLTableCellElement                 |
| thead                          |   HTMLTableSectionElement                 |
| title                          |   HTMLTitleElement                 |
| tr                          |   HTMLTableRowElement                 |
| tt                          |   HTMLElement                 |
| ul                          |   HTMLUListElement                 |
| var                          |   HTMLElement                 |


##2. 取得特性

> 每个元素都有一或多个特性，这些特性的用途是给出相应元素或其内容的附加信息，操作特性的DOM方法：
+ getAttribute
+ setAttribute
+ removeAttribute

```javascript

var div = document.getElementById("myDiv");
alert(div.getAttribute("id")); //"myDiv"
alert(div.getAttribute("class")); //"bd"
alert(div.getAttribute("title")); //"Body text"
alert(div.getAttribute("lang")); //"en"
alert(div.getAttribute("dir")); //"ltr"

```

***不过，特性的名称是不区分大小写的，即"ID"和"id"代表的都是同一个特性。另外也要注意，根据 HTML5 规范，自定义特性应该加上 data-前缀以便验证***


> HTMLElement 也会有 5个属性与相应的特性一一对应，只有工人的特性才会以属性的形式添加到DOM对象中：

```
<div id="myDiv" align="left" my_special_attribute="hello!"></div>
```

```javascript

alert(div.id); //"myDiv"
alert(div.my_special_attribute); //undefined（ IE 除外）
alert(div.align);
```







