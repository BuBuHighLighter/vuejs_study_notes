# 其他指令的使用

## v-once

该指令后面不需要跟任何表达式。

该指令表示元素和组件只渲染一次，不会随着数据的改变而改变。

[代码示例](../demos/demo1/index.html)
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

[代码示例](../demos/demo2/index.html)

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

[代码示例](../demos/demo3/index.html)

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

[代码示例](../demos/demo4/index.html)

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

[代码示例](../demos/demo5/index.html)

```html
<div id="app">
    <h1>{{message}}</h1>
    <h1 v-cloak>{{message}}</h1>
</div>

<script>
    setTimeout(() => {const app = new Vue({
        el: '#app',
        data: {
            message: 'hello world'
        }
    })}, 1000);
</script>
```