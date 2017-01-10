# 概要

#### 元素
1. 替换元素：用来替换元素内容的部分，非由文档内容直接表示.(img、input)
2. 非替换元素
    + 块级元素：默认生成一个框，并填充父级元素内容区，并旁边不能有其他元素
    + 行内元素

#### link

```html
<link rel="stylesheet" type="text/css" href="style.css">
```

media 属性：
+ all
+ print
+ screen
+ tv

#### @import

```html
<style type="text/css">
    @import url('css1.css');
    @import url('css2.css');
    h1{
        font-size:22px;
    }
</style>
```

***允许@import多个文件，但必须放到所有style的最前面，否则不生效***

#### 属性选择器

#####1. 简单的属性名选择

```style
h1[title]
p[name]
div[data-id]
div[require]
```

通过属性名字（包括自定义属性）进行选择，扩展选择空间

#####2. 属性和属性值

```
h1[data-name='lin']
div[data-box='dp']
```

通过对属性与属性值的完全匹配进行选择

#####3. 属性和部分属性值

>使用~波浪号，当属性值都具有空格隔开的值时，容易进行帅选 

```
div[class~='waining']
div[title~='link']
```

完全属性名称和部分属性值进行选择

#####4. 属性和任意包含属性值

> 使用*号，当属性值包含任意选择器中的值都可以被选中

```
div[placeholder*='请']{
    border:solid 1px yellow;
    outline: 1px rebeccapurple inset;
}
```

#####5. 属性和任意开头结尾

```
div[title^='my']
div[title$='over']
```

#####6. 特定元素选择器

```
div[lang|='en']

```

选择en或en-au开头的所有元素

#### 结构选择器

#####1. 选择子元素

```
h1 > strong {
    color:red;
}
```

上述选择器，只会选择h1元素直属子元素，而不会选择后代中的strong子元素

```html
<h1>this is very <strong>Goods</strong></h1>
<h1>this is <em>very <strong>Goods</strong></em></h1>
```

上述html中，第一个h1的strong会被选择，而第二个则不会

#####2. 兄弟元素选择器

> 相邻兄弟结合符，这表示为一个加号（+）

假设有如下结构：
```html
<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
</ul>
<ol>
    <ol>A</ol>
    <ol>B</ol>
    <ol>C</ol>
</ol>
```

采用如下样式选择器
```css
/*选择ul兄弟节点 ol*/
ul + ol{
    list-style:none;
}

/*选择兄弟元素有两个相邻的li元素，第一个li不会被选择*/
ul>li+li{
    border:solid 1px #888;
}

/*选择相邻的ol，第一个ol不会被选择*/
ol + ol{
    font-weight:bold;
    color:#887324;
}

```

#### 伪类

#####1. 静态伪类

```css
a:link{}
a:visited{}
```

#####2. 动态伪类

```css
a:hover{}
a:focus{}
a:active{}
```

#####3. 位置伪类

```css
div:first-child{}
div:last-child{}
```

注意：***针对选中div中的第一个/最后一个div进行选择***

#### 伪元素

```css
p:before{
    content:''
}
p:after{
    content:''
}
```

伪元素常用，做一些特殊的效果

#### 样式特殊性

+ ID选择器优先级最高，加4分
+ 类属性值，属性选择或伪类，加2分
+ 元素名称和伪类，加1分




