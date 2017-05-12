# Array 

## 常用函数

### 增删插替

+ Array.prototype.push   新增至元素尾部，返回长度
+ Array.prototype.unshift 新增元素至数组首部，返回长度
+ Array.prototype.pop    删除最后一个元素并返回删除元素
+ Array.prototype.shift  删除第一个元素并返回删除元素
+ Array.prototype.splice 删除指定位置元素或替换元素，并返回删除元素Array

### 获取新数组

+ Array.prototype.concat 连接多个数组，返回一个新数组
+ Array.prototype.slice  获取指定位置字数组，返回一个新数组
+ Array.prototype.map    遍历元素生成新数组
+ Array.prototype.filter 过滤元素生成新数组

### 循环

+ Array.prototype.forEach 遍历数组元素
+ Array.prototype.reduce  遍历数组，累积结果集
+ Array.prototype.reduceRight 从右边开始遍历数组，累积结果集

### 查找

+ Array.prototype.indexOf 获取相匹配元素第一个索引值
+ Array.prototype.lastIndexOf 获取相匹配元素匹配最后一个索引值
+ Array.prototpye.findIndex   获取相匹配元素第一个索引值
+ Array.prototpye.find  获取相匹配的第一个元素

### 条件检验

+ Array.prototype.every  每个元素都满足返回true，否则返回false
+ Array.prototype.some   有元素满足返回true，否则返回false
+ Array.isArray 是否为数组

### 排序与反转

+ Array.prototype.sort 数组排序
+ Array.prototype.reverse 数组元素反转

### 生成字符串

+ Array.prototype.join 将元素生成字符串，采用指定字符作为连接符
+ String.prototype.split 相反

### ES6新增

+ Array.from 将类数组转换成数组
+ Array.of   将指定值元素创建新数组
