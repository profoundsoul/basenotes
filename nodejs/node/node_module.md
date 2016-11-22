# 模块机制

## 传统Web1.0 JS脚本作用
+ 表单验证
+ 特效

## JS先天缺陷

+ 模块化系统，有的更多的是script标签太过于零散
+ 统一标准库极少，例如IO、文件等库
+ 缺乏包管理系统

## CommonJS的模块规范

+ 模块引用，require 
+ 定义模块，在node中一个文件就是一个模块。exports 或module.exports 对象为一个模块导出对象。
+ 模块标识，通过具体标识或文件路径，可以不加js后缀

## Node引入模块步骤
+ 路径分析-找到名字相同的文件或包;node-modules
+ 文件查找-根据文件或目录、包找到具体的后缀文件;package.json
+ 编译执行-将node模块编译成二进制且执行;不同后缀编译方式不一样

***Nodejs对CommonJS实现增强了模块标识定位（路径分析、文件定位）、增加了模块编译及缓存策略提升性能***

常见的Node模块分为两类：
+ 核心模块，模块标识加载具有除缓存外最高优先级；不经文件定位、编译执行。
+ 文件模块，以文件路径为主的模块
+ 自定义模块，非路径形式的模块标识符，查找最费时，需逐级查找node_modules查找相应的包或模块

***webpack、babel、jquery、vue、react、net等库都是自定义模块，通常都是在node_modules中查找***

## 模块加载：
+ 优先从缓存中加载模块
+ 模块标识符分析
    - 核心模块
    - 文件模块
    - 自定义模块，最难以查找；查找node_modules文件目录，并逐级往父级查找，直到找到为止。

***自定义模块查找与JavaScript原型链查找相似，当前文件路径越深，查找越费时***

+ 文件定位
    - node会按照.js、 .json、 .node以此查找
    - 优先查找package.json文件中的main节点。如果不存在默认依次查找为 index.js、 index.json、 index.node等文件

## 模块编译

编译和执行是引入文件模块的最后一个阶段，对应不同的文件拓展名。具有不同的编译方式：
+ js 通过fs模块同步读取文件后编译执行
+ node 这是C/C++的拓展文件，通过dlopen方法加载最后编译生成的文件
+ json 通过fs模块同步读取文件后，使用JSON.parse解析返回结果
+ 其余文件都当成js文件进行解析


### JS文件模块编译

> 按照CommonJS规范，每个模块必须拥有require、module、exports三个变量，但js文件中并没有定义。从何而来？甚至NodejsAPI中还存在__filename、__dirname这两个变量，又从何而来呢？

#### 头尾包装

```javascript
(function(module, require, exports, __filename, __dirname){
    
});
```

常见包装后代码：

```javascript
(function(exports, require, module, __filename, __dirname){
    var math = require('math');
    exports.area = function (radius) {
    return Math.PI * radius * radius;
    };
});
```

