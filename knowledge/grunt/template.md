# Grunt Template机制

grunt为了更方便组合路径等格式化文本，采用了underscore(_)的template模板机制，如果不熟悉可以参考[underscore官网](http://underscorejs.org/#template)

## template 基本用法

简单介绍下模板，主要有三个标签:
+ <% %> 定义js脚本
+ <%= %> 将js变量中的文本写入字符串中
+ <%- %>  内容带有html-escaped写入字符串中

```javascript
var compiled = _.template("hello: <%= name %>");
compiled({name: 'moe'});
## => "hello: moe"

var template = _.template("<b><%- value %></b>");
template({value: '<script>'});
## => "<b>&lt;script&gt;</b>"


## 改变<%  %>模板写法为{{  }}
_.templateSettings = {
  interpolate: /\{\{(.+?)\}\}/g
};

```

## Config中可用变量







