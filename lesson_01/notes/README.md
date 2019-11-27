# 邂逅Vuejs

## 认识Vuejs

Vue是一个渐进式框架，什么是渐进式？

- 渐进式意味着你可以将Vue作为你应用的一部分嵌入其中，带来更丰富的交互体验。
- 或者如果你希望将更多的业务逻辑使用Vue实现，那么Vue的核心库以及其生态系统。
- 比如Core+Vue-router+Vuex，也可以满足你各种各样的需求。

Vue有很多特点和Web开发中常见的高级功能

- 解耦视图和数据
- 可复用的组件
- 前端路由技术
- 状态管理
- 虚拟DOM

安装Vue的方式

- 方法一：直接CDN引入
- 
  ```html
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <!-- 生产环境，优化了尺寸和速度 -->
    <script src="https://cdn.jsdelivr.net/npm/vue"></script>
  ```
- 方法二：下载和引入
- 
  开发环境: https://vuejs.org/js/vue.js

  生产环境: https://vuejs.org/js/vue.min.js

- 方法三：NPM安装
  后续通过CLI和webpack的使用，使用该方法。

[一个计数器案例](../demos/demo3/index.html)

Vue中的MVVM

![MVVM](./imgs/MVVM.png)

## v-once

该指令后面不需要跟任何表达式。

该指令表示元素和组件只渲染一次，不会随着数据的改变而改变。

[代码示例](../demos/demo4/index.html)
```html
<div id="app">
  <h1>{{message}}</h1>                <!-- 123 -->
  <h1 v-once>{{message}}</h1>         <!-- hello world -->
</div>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: 'hello world'
    }
  })

  app.message = '123';
</script>
```

## v-html

该指令后面往往会跟上一个string类型。

会将string的html解析出来并且进行渲染。

[代码示例](../demos/demo5/index.html)

```html
<div id="app">
  <h2>{{url}}</h2>
  <h2 v-html="url"></h2>
</div>

<script>
  const app = new Vue({
    el: '#app',
      data: {
      url: '<a href="http://www.baidu.com">百度</a>'
    }
  })
</script>
```

## v-text

v-text作用和Mustache比较相似：都是用于将数据显示在界面中。

v-text通常情况下，接受一个string类型。

[代码示例](../demos/demo6/index.html)

```html
<div id="app">
  <h1>{{message}}123</h1>               <!-- hello world123 -->
  <h1 v-text="message">123</h1>         <!-- hello world -->
</div>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: 'hello world'
    }
  })
</script>
```

## v-pre

v-pre用于跳过这个元素和它子元素的编译过程，用于显示原本的Mustache语法。

[代码示例](../demos/demo7/index.html)

```html
<div id="app">
  <h1>{{message}}</h1>                <!-- hello world -->
  <h1 v-pre>{{message}}</h1>          <!-- {{message}} -->
</div>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: 'hello world'
    }
  })
</script>
```

## v-cloak

cloak：斗篷

在某些情况下，我们浏览器可能会直接显示出未编译的Mustache标签。

即为渲染之前显示未编译的Mustache标签，渲染之后才显示变量内容，会存在一个闪动，使用该命令能让未渲染之前不显示Mustache标签不显示，待到渲染之后才显示真正的内容。

- 在vue解析之前，div中有一个属性v-cloak
- 在vue解析之后，删除div中的v-cloak属性

大致原理如下：

```css
[v-cloak] {
  display: none;
}
```