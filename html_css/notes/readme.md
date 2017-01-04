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

#####2. 
