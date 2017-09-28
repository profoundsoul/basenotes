# Vue2分享

* Vue2核心基础知识

* 组件系统（props、emit events、slot）

* 扩展能力-插件

* webpack模块捆绑器

* babel/es6

---

## Vue2基础

* Vue2实例生命周期

* 模板及指令

* 响应式属性-数据驱动（data、watch、computed）

---

### Vue2实例生命周期

> 每个 Vue 实例在被创建之前都要经过一系列的初始化过程。例如需要设置数据监听、编译模板、挂载实例到 DOM、在数据变化时更新 DOM 等。同时在这个过程中也会运行一些叫做**生命周期钩子**的函数，给予用户机会在一些特定的场景下添加他们自己的代码

* Created
> 到该钩子执行，Vue实例已经完成：初始化事件、响应式data。
* mounted
> 到该钩子执行，Vue实例已经完成template模板编译、挂载到el跟节点。此时Vue的内容在html文档DOM树中

---

* updated

> 执行该钩子，Vue实例中响应式数据（data、computed等）发生变化，更新VDom及重新渲染HTML 文档DOM

* destroyed

> 执行该钩子，Vue实例被销毁（Watcher、components、event Listeners等均被销毁）

**Remind**：上述主要钩子中，每个钩子均存在一个before的钩子（beforeCreate、beforeMount、beforeUpdate、beforeDestroy）处理特殊场景

---

图谱：![](/assets/lifecycle111111.png)

---

### 模板及指令

> Vue.js 使用了基于 HTML 的模板语法，允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。所有 Vue.js 的模板都是合法的 HTML ，所以能被遵循规范的浏览器和 HTML 解析器解析。
>
> 在底层的实现上，Vue 将模板编译成虚拟 DOM 渲染函数。结合响应系统，在应用状态改变时，Vue 能够智能地计算出重新渲染组件的最小代价并应用到 DOM 操作上。

* 文本

```html
<span>Message: {{ msg }}</span>
```

* v-html 原始html

```html
<div v-html="rawHtml"></div>
```

---

* v-bind或:简写

```html
<button :title="tips"></button>
<a v-bind:href="url"></a>
<div v-bind:class="{ active: isActive }"></div>
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
```

* v-on或@简写

```html
<a @click="doSomething(username, $event)"></a>
<a @click="doSomething('first')"></a>
<a @click.prevent="doSomething('first')"></a>
```

---

* v-model

```html
<input v-model="message" placeholder="edit me">
<input type="checkbox" id="checkbox" v-model="checked">
<input type="radio" id="one" value="One" v-model="picked">
<input type="radio" id="two" value="Two" v-model="picked">
<input v-model.number="age" type="number">
<input v-model.trim="msg">
```

---

* v-if/v-else/v-else-if

```html
<h1 v-if="ok">Yes</h1>
<h1 v-else>No</h1>

<template v-if="ok">
<h1>Title</h1>
<p>Paragraph 1</p>
<p>Paragraph 2</p>
</template>
```


* v-show

```html
<h1 v-show="ok">Hello!</h1>
```

---

**Remind**：

#### v-if vs v-show 区别

* v-if 懒惰，条件为真时才渲染，可以用来做**懒惰加载组件或弹窗**
* v-show 只是相当于style='display:none'，**频繁渲染且变化不大的组件**

#### v-if 与 v-for一起使用

* v-for有更高的优先级，处理它们是可以建议使用template

```html
<template v-if='list.length'>
<li v-for='item in list'>{{item}}</list>
</template>
```

---

### 响应式属性

> Vue 的一个最明显的特性就是其不太引人注意的响应式系统。数据模型仅仅是普通的  对象。而当你修改它们时，视图会进行更新。当你把一个普通的  对象传给 Vue 实例的`data`选项，Vue 将遍历此对象所有的属性，并使用[Object.defineProperty](https://developer.mozilla.org/en-US/docs/Web//Reference/Global_Objects/Object/defineProperty)把这些属性全部转为 getter/setter。

* data数据会被代理，拥有通知watcher的能力

---

#### 实现原理

> 每个组件实例都有相应的**watcher**实例对象，它会在组件渲染的过程中把属性记录为依赖，之后当依赖项的`setter`被调用时，会通知`watcher`重新计算，从而致使它关联的组件得以更新。

* Data中数据相当发布者（publish）
* 而VDom相当于watcher订阅者（subscribe）

数据实现由Model Data更新Dom节点

* VDom Listener事件订阅（input），更新Data数据
* 用户文本框输入，HTML节点发布事件

---

![](/assets/data11111.png)


---

#### computed

> 模板内的表达式是非常便利的，但是它们实际上是用于简单运算的。在模板中放入太多的逻辑会让模板过重且难以维护，而且data中的属性都具有观察能力，性能和实现难度都会加大。

* 同时观察多个响应式数据
* 缓存数据的能力

---

```javascript
var vm = new Vue({
        el: '#demo',
        data: {
        firstName: 'Foo',
        lastName: 'Bar'
    },
    computed: {
        fullName: function () {
            return this.firstName + ' ' + this.lastName
        }
    }
})
```

---

#### watch

> Vue 确实提供了一种更通用的方式来观察和响应 Vue 实例上的数据变动：**watch 属性**。当你有一些数据需要随着其它数据变动而变动时

```javascript
var vm = new Vue({
        el: '#demo',
        data: {
        firstName: 'Foo',
        lastName: 'Bar',
        fullName: 'Foo Bar'
    },
    watch: {
        firstName: function (val) {
            this.fullName = val + ' ' + this.lastName
        },
        lastName: function (val) {
            this.fullName = this.firstName + ' ' + val
        }
    }
})
```


---

**Q**：

+ data一级属性什么时候定义,为什么？
+ watch可以监听那些属性 ,data中的二级属性能否监听？
+ data属性是响应式的，如果操作二级属性（数组、对象、简单数据类型）依然让它们具有响应的能力