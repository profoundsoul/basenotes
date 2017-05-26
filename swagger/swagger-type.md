# Swagger Type And Rule

## Data Type

> 常用的Primitive Date Type 及复杂数据类型：
> + integer
> + number
> + string 
> + boolean
> + object
> + array

#### default

>指定当前属性的默认值，优先高于一切值

```yaml
defaultstr:
  description: 指定具体默认值
  type: string
  x-range: 20
  default: xxxxxxxxx
  minLength: 5
  maxLength: 20
```

**注意：**此时x-range、minLength、maxLength失效等所有的特性均失效

#### Enum

> 为数组类型，里面允许指定具体的数值或项，枚举值优先级高于自定义规则


```yaml
enumstr:
  description: 枚举值优先随机选择
  type: string
  enum: [sds,人民,笑话,天朝,韩流,谈人生谈理想]
```

**注意：**优先级高于其它规则，只低于default值。有此项时，随机从enum中取出一项值

### Array

> 数组允许控制数据条数：
> + minimum 最小数据条数
> + maximum 最大数据条数

```yaml
recommendBrandList:
    description: really
    properties:
      brand_list:
        description: really
        type: array
        minimum: 5
        maximum: 10
        items:
          "$ref": "#/definitions/recommendBrand"
    type: object
```


### integer
> 最大值和最小值范围：
> + minimum 最小数值，整数
> + maximum 最大数值，整数

应对MockJS中随机生成数据规则/函数：Random.integer(min?, max?)

```javascript
//正常情况对应最小值和最大值
Random.integer(min?, max?)

//如果只填写minimum
Random.integer(min?)

//如果没有填写范围
Random.integer()
```

```yaml
integer:
  description: 返回码
  type: integer
  minimum: 0
  maximum: 10
```

### number

> 最大值和最小值范围：
> + minimum 最小数值，整数
> + maximum 最大数值，整数
> + x-digit 小数点位数


应对MockJS中随机生成数据规则/函数:Random.float( min?, max?, dmin?, dmax? )

```javascript
//不填写随机生成浮点型数值
Random.float()

//只填写minimum
Random.float(0)

// minimum 与 maximum
Random.float(60, 100)

// minimum 与 maximum及x-digit为单数值，无逗号分隔。例如：3
Random.float(60, 100, 3)

// Random.float( min, max, x-digit )
// x-digit 是两个数值且以逗号分隔，例如：3,5
Random.float(60, 100, 3, 5)
```

```yaml
number:
  description: 浮点
  type: number
  minimum: 0
  maximum: 20000
  x-digit: 2,4   
price:
  description: 价格
  type: number
  minimum: 100
  maximum: 10000
  x-digit: 2
```

### String

> 允许指定长度范围：
> + minLength
> + maxLength
> + x-range    取值范围字符串或指定转换字符
>   + lower    小写字母
>   + upper    大写字母
>   + number   数值
>   + symbol   特殊字符
>   + 随机字符串，后面长度范围在此处任选字符串

应对MockJS中随机生成数据规则/函数：Random.string( pool?, min?, max? )

```javascript
Random.string()

//只填写minLength或maxLength时，表示随机出来字符串长度。例如：minLength为5
Random.string(5)

//minLength与maxLength
Random.string(7, 10)

//x-range的值为lower项，表示生成小写字母，随机生成5小写字母
Random.string('lower', 5)

//x-range的值为uppper项，表示生成大写字母， 随机生成5小写字母
Random.string('upper', 5)

//x-range的值为number项，表示生成0-10数字，随机生成5数字字符
Random.string('number', 5)

//x-range的值为symbol项，表示生成特殊字符，随机生成5数字字符
Random.string('symbol', 5)

//x-range的值为其它时，表示生成自定义字符集，字符从自定义字符集中取值，允许重复
Random.string('aeiou', 5)

// Random.string( pool, min, max )
// x-range的值为lower项，minLength和maxLength均填写时，随机生成1-3位小写字母
Random.string('lower', 1, 3)

// x-range的值为其它项，minLength和maxLength均填写时，随机生成1-3位指定字符串集内的字符
Random.string('qwertyuiop[]\;', 1, 3)
```

```yaml
uppperstr:
  description: 返回错误消息
  type: string
  x-range: 'upper'
  minLength: 10
  maxLength: 30
customstr:
  description: 自定义字符串
  type: string
  x-range: abdedfkglpoiyuwq1234567890
  minLength: 20
  maxLength: 40
```

### String与x-format=guid 随机md5码

```javascript
Random.guid()
```

```yaml
guid:
  description: GUID
  type: string
  x-format: guid
```

### String与x-format=id   随机id

```javascript
Random.id()
```

```yaml
id: 
  description: id
  type: string
  x-format: id
```

### String与x-format=step   自增长ID

> 允许指定每次的增量值：
> x-step 整数, 表示增量数值 

```javascript
Random.increment( step? )

```

```yaml
step:
  description: 自增长字符串
  type: string
  x-format: step
  x-step: 2
```

### String与x-format=title 英文标题

> 允许指定英文标题的长度范围：
> + minLength  最小长度
> + maxLength  最大长度

```javascript
Random.title( min?, max? )
```

```yaml
title:
  description: 英文标题
  type: string
  x-format: title
  minLength: 15
```

### String与x-format=ctitle 中文标题

> 允许指定中文标题的长度范围：
> + minLength  最小长度
> + maxLength  最大长度

```javascript
Random.ctitle( min?, max? )
```

```yaml
ctitle:
  description: 中文标题
  type: string
  x-format: ctitle
  minLength: 2
```

### String与x-format=text   英文备注

> 允许指定文本的段落数目范围：
> + minLength  最小段落数
> + maxLength  最大段落数

```javascript
Random.paragraph( min?, max? )
```

```yaml
text:
  description: 大段落文本英文
  type: string
  x-format: text
  minLength: 2
```

### String与x-format=ctext   中文备注

> 允许指定文本的段落数目范围：
> + minLength  最小段落数
> + maxLength  最大段落数

```javascript
Random.cparagraph( min?, max? )
```

```yaml
ctext:
  description: 中文文本
  type: string
  x-format: ctext
  minLength: 3
```

### String与x-format=cname  中文名字

```javascript
Random.cname()

```

```yaml
cname:
  description: 中文用户名称
  type: string
  x-format: cname
```

### String与x-format=name   英文名字

```javascript
Random.name()
```

```yaml
name:
  description: 英文名字
  type: string
  x-format: name
```

### String与x-format=email  邮件

> 允许指定email的域名：
> x-domain 指定域名

```javascript
Random.email(x-domain?)
```

```yaml
email:
  description: 电子邮件
  type: string
  x-format: email
  x-domain: 163.com
```

### String与x-format=date   日期

> 对于返回具体日期格式数据：
> + x-style 默认值为yyyy-MM-dd，允许自己自定义

```javascript
Random.date( x-style? )
```

```yaml
date:
  description: 日期
  type: string
  x-format: date
  x-style: yyyy/MM/dd
```

### String与x-format=time   时间

> 对于返回具体时间格式数据：
> + x-style 默认值为HH:mm:ss，允许自己自定义

```javascript
Random.time( x-style? )
```

```yaml
time: 
  description: 时间
  type: string
  x-format: time
  x-style: HH:mm:ss
```

### String与x-format=date-time 日期和时间

> 对于返回具体日期时间格式数据：
> + x-style 默认值为yyyy-MM-dd HH:mm:ss，允许自己自定义

```javascript
Random.datetime( x-style? )
```

```yaml
datetime:
  description: 日期时间
  type: string
  x-format: datetime
  x-style: yyyy/MM/dd HH:mm
```

### String与x-format=now 当前日期和时间

> 对于返回具体日期时间格式数据：
> + x-style 默认值为yyyy-MM-dd HH:mm:ss，允许自己自定义


```javascript
Random.now( x-style? )
```

```yaml
now:
  description: 当前日期时间
  type: string
  x-format: now
  x-style: yyyy/MM/dd HH
```

### String与x-format=url URL

> 允许指定URL的协议名称和主机名称：
> + x-protocol 协议名称
> + x-host 主机名称

```javascript
Random.url(protocol, host)

```

```yaml
url:
  description: 超链接
  type: string
  x-format: url
  x-protocol: http
  x-host: yiwill.com
```

### String与x-format=image 超链接地址

> 允许指定图片大小，背景，字体颜色，图片类型，图片上的文本等信息
> + x-style的值有如下规则，多个属性值采用逗号分隔: 
>   + size
>   + size, background
>   + size, background, text
>   + size, background, foreground, text
>   + size, background, foreground, format, text

```javascript
// Random.image()
Random.image()
// Random.image( size )
Random.image('200x100')
// Random.image( size, background )
Random.image('200x100', '#FF6600')
// Random.image( size, background, text )
Random.image('200x100', '#4A7BF7', 'Hello')
// Random.image( size, background, foreground, text )
Random.image('200x100', '#50B347', '#FFF', 'Mock.js')
// Random.image( size, background, foreground, format, text )
Random.image('200x100', '#894FC4', '#FFF', 'png', '!')
```

```yaml
image:
  description: 图片地址
  type: string
  x-format: image
  x-style: 200x200,#ccc,#222,png,test
```

### String与x-format=regexp 自定义正则表达式

> 如果上面所有情况都满足不了，可以使用x-range定义正则表达式：
> x-range: 写js正则表达式，忽略gi等配置参数

```javascript
Mock.mock(regexp?)

```

```yaml
regexp:
  description: 自定正则表达式
  type: string
  x-format: regexp
  x-range: /[\w]{15,}/
customreg:
  description: 自定正则表达式
  type: string
  x-format: regexp
  x-range: /[\d的是个的风格就那样的风格的方式]{15,}/
```
