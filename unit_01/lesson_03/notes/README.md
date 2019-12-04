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

绑定class有两种方法：

- 对象语法
- 数组语法

对象语法有下面这些用法：

- 用法一：直接通过`{}`绑定一个类

```html
<h2 :class="{'active': isActive}">Hello world</h2>
```

- 用法二：也可以通过判断，传入多个值

```html
<h2 :class="{'active': isActive, 'line': isLine}">Hello world</h2>
```

- 用法三：和普通的类同时存在，并不冲突

```html
<h2 class="title" :class="{'active': isActive, 'line': isLine}">Hello world</h2>
```

- 用法四：如果过于复杂，可以放在一个methods或者computed中
  
  注：classes是一个计算属性

[代码示例](../demos/demo4/index.html)
```html
<h2 class="title" :class="classes">Hello world</h2>
```

## v-bind动态绑定class(数组语法)

数组语法的含义是:class后面跟的是一个数组。

数组语法其实是写死的，只是可以通过methods或computed返回一个数组（即通过操作该数组实现动态类名）。

如果数组元素不加单引号，他会当成一个变量去解析。

```html
<div id="app">
    <!-- class="title active line" -->
    <span class="title" :class="['active', 'line']">Hello world</span>
    <!-- class="title aaa bbb" -->
    <span class="title" :class="[active, line]">Hello world</span>
    <!-- class="title active line" -->
    <span class="title" :class="computedClasses">Hello world</span>
    <!-- class="title aaa bbb" -->
    <span class="title" :class="getClasses()">Hello world</span>
</div>

<script>
    const app = new Vue({
        el: '#app',
        data: {
            active: 'aaa',
            line: 'bbb',
        },
        methods: {
            getClasses() {
                return [this.active, this.line];
            }
        },
        computed: {
            computedClasses() {
                return ['active', 'line'];
            }
        }
    })
</script>
```

数组语法有下面这些用法：

- 用法一：直接通过`[]`绑定一个类

```html
<h2 :class="['active']">Hello world</h2>
```

- 用法二：也可以传入多个值

```html
<h2 :class="['active', 'line']">Hello world</h2>
```

- 用法三：和普通的类同时存在，并不冲突
  
  注：会有title、active、line三个类

```html
<h2 class="title" :class="['active', 'line']">Hello world</h2>
```

- 用法四：如果过于复杂，可以放在一个methods或者computed中
  
  注：classes是一个计算属性

```html
<h2 class="title" :class="classes">Hello world</h2>
```

