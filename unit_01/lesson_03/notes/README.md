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