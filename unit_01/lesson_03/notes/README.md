# v-bind

作用： 动态绑定属性

缩写： `:`

预期：any(with argument) | Object(without argument)

参数：attrOrProp(optional)

v-bind用于绑定一个或多个属性值，或者向另一个组件传递props值。

[代码示例](../demos/demo1/index.html)

```html
<div id="app">
    <!-- 普通写法 -->
    <img v-bind:src="imgUrl">
    <a v-bind:href="aHref">123</a>

    <!-- 语法糖写法 -->
    <img :src="imgUrl">
    <a :href="aHref">123</a>
</div>

<script>
    const app = new Vue({
        el: '#app',
        data: {
            imgUrl: 'https://i0.hdslb.com/bfs/archive/d8852d6a99de0e9a4c585c0c610fd4c80c957657.jpg@336w_190h.webp',
            aHref: 'http://www.baidu.com'
        }
    })
</script>
```

## v-bind动态绑定class(对象语法)

先绑定一个普通的class。

[代码示例](../demos/demo2/index.html)
```html
<div id="app">
    <div class="redDiv">hello world1</div>          <!-- class=redDiv -->
    <div :class="className">hello world2</div>      <!-- class=redDiv -->
</div>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            className: 'redDiv'
        }
    })
</script>
```

也可以通过对象的形式传入class，对象是键-值对的形式，值为true，则显示键名的class属性。

[代码示例](../demos/demo3/index.html)

```html
<div id="app">
    <!-- 显示class="redDiv line" -->
    <div :class="{redDiv: value1, line: value2}">hello world</div>
</div>

<script>
    const app = new Vue({
        el: '#app',
        data: {
            value1: true,
            value2: true
        }
    })
</script>
```

