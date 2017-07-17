# Vue2.0 特性

## 基础属性

+ Vue实例构造函数，初始化以下数据
    + options.props     作为组件入参，先验证后代理观察属性
    + options.methods   将具体method挂vm实例中，并将this指向vm
    + options.data      作为基础数据，代理观察属性
    + options.computed  作为计算属性，代理观察（只有Getter无Setter）
    + options.watch     作为观察属性，代理观察已有属性（存在Setter）
+ 代理属性和方法($data 是响应式的)
    + Vue实例暴露了一些有用的实例和方法，这些实例和方法都有前缀$,以便区分代理属性
    + 不用再实例属性或回调函数使用=>箭头函数
+ 实例生命周期
    + *beforeCreate*
    + observe data
    + init Events
    + *created*
    + compile template
    + *beforeMount*
    + create el and replace el
    + *mounted*
    + *before Update*
    + Virtual Dom re-Render
    + *updated*
    + *beforeDestory*
    + teardown watchers/component/events, destoryed
    + *destoryed*
+ html 模板语法

## 模板语法


### 插值
+ {{}}
+ v-html
+ v-bind:title   :
+ v-on:click     @

*支持原生单语句表达式(复杂表达式，多语句表达式，变量定义均不能执行)*


### 指令

+ v-for
+ v-if v-else v-else-if

### 组件模板

+ is特性
    + 主要是为了解决html中一些特定元素只能包含指定元素，例如：
        + table tr td 组合
        + ul li (ol dd dl)组合
        + select option 组合
        + a/span标签不允许放快级子元素
    ```html
    <table>
      <tr is="my-component"></tr>
    </table>
    ```
+ slot占位符

## 组件

+ data 必须是函数返回数值
+ props 定制入参，使用组件时v-bind或:进行传值
    + 参数名称
    + 数据类型type，允许多中数据类型（Object、Number、Boolean、String、Function、Array、Symbol）
    + 数据验证，required、validator函数等
    + 默认值default
+ $on与$emit自定义事件
+ slot 内容分发
    + 编译作用域（父组件或容器的作用域)
    + 默认slot，组件innerHtml全部放入
    + 带名字slot，模板页指定()
    + 作用域插槽，允许往slot中传值，在使用时指定scope为具体属性名称
+ $ref 访问子组件



