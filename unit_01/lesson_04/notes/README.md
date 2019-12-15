# 计算属性

## 计算属性的基本使用

computed是计算属性，所以在使用computed的时候，要使用给属性起名的方法来给计算属性命名，而不是用方法命名方法（例如：get/set）。直接使用`fullName`之类的名称给计算属性命名。

**methods和computed看起来都差不多，为什么要用计算属性？**

计算属性会进行缓存，如果多次使用，计算属性只会调用一次，而methods每次都会调用。


## 计算属性的setter和getter

每个计算属性都包含一个`getter`和一个`setter`。

一个完整的计算属性:

```html
<script>
    const app = new Vue({
        el: '#app',
        data: {
            message: 'hello world'
        },
        computed: {
            fullName: {
                get: function() {

                },
                // 一般情况下不需要实现set方法。没有set方法就是一个只读属性。
                // set方法是个有参数的方法
                set: function(newValue) {

                }
            }
        }
    })
</script>
```

简写的计算属性:

```html
<script>
    const app = new Vue({
        el: '#app',
        data: {
            message: 'hello world'
        },
        computed: {
            fullName: function() {

            }
        }
    })
</script>
```

[一个完整的示例](../demos/demo1/index.html)

## 计算属性和methods的对比

[代码示例](./../demos/demo2/index.html)
```html
<div id="app">
    <!-- 调用4次getFullName() -->
    <span>{{getFullName()}}</span>
    <span>{{getFullName()}}</span>
    <span>{{getFullName()}}</span>
    <span>{{getFullName()}}</span>

    <!-- 调用1次fullName -->
    <span>{{fullName}}</span>
    <span>{{fullName}}</span>
    <span>{{fullName}}</span>
    <span>{{fullName}}</span>
</div>

<script>
    const app = new Vue({
        el: 'app',
        data: {
            firstName: 'Kobe',
            lastName: 'Bryant',
        },
        methods: {
            getFullName() {
                console.log('getFullName()');
                return this.firstName + ' ' + this.lastName;
            }
        },
        computed: {
            fullName() {
                console.log('fullName');
                return this.firstName + ' ' + this.lastName;
            }
        }
    })
</script>
```

计算属性会做一层缓存，如果底层数据(firstName/lastName)没有改变，则不需要重新计算，直接从缓存中获取值。
