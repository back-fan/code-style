# Vue-Style-Guide

> 遵循elint规范，vue官方风格指南

### 1 Vue属性书写顺序

```html
  <div ref="div" v-if="isShow">
    <el-tag
      v-for="(item, index) in tagList"
      :key="item.name + index"
      :type="item.type"
      closable
      class="new-class"
      @click="handleClick"
    >
      <!-- 
        注：不建议在html中写大片的、换行的注释
        属性值为布尔值时，根据默认值去简写。
        例如：closable默认值为false，需要使用closable对应的功能时，简写为‘closable’，而不是'closable: true'。默认值为true时则不写，不需要使用对应功能时为':closable: false'。
      -->
      <span>{{ item.name }}</span>
    </el-tag>
  </div>
```

```javascript
export default {
  mixins,
  components,
  props,
  data,
  computed，
  watch,
  route,
  created, // => 生命周期顺序不赘述
  ready,  
  methods
}
```

### 2 组件

#### 2.1 命名

组件以驼峰命名

```html
<template>
  <my-components></my-components>
</template>

<script>
  import myComponents from './myComponents.vue'

  export default {
  components: {
  	  myComponents
    }
  }
</script>

<style>
</style>
```

#### 2.2 Vue组件的书写顺序
建议：template script style 的顺序书写，都要换行
```vue
<template></template>

<script></script>

<style></style>
```
#### 2.3 组件引用

```javascript
  import myComponentsA from './myComponentsA.vue'  
  import myComponentsB from './myComponentsB.vue'
  import myComponentsC from './myComponentsC.vue'
  import myComponentsD from './myComponentsD.vue'

  export default {
    components: {
  	  myComponentsA,
      myComponentsB,
      myComponentsC,
      myComponentsD,
    }
  }
```

### 3 事件

```html
<!-- bad -->
<a v-on:click="pass()">pass</a>

<!-- good -->
<a @click="pass">pass</a>

```

### 4 优先级

* 组件名多个单词组成

> 原因：避免跟现有的以及未来的HTML元素冲突，并且HTML元素名称都是单个单词。

* prop定义尽量详细，至少指定类型

``` javascript
// bad
props: ['status']

// good 
props: {
  status: {
    type: String,
    default: 'some string'
  }
}

// best
props: {
  status: {
    type: String,
    require: true,
    validator: function (value) {
      return [
        'syncing',
        'synced',
        'version-conflict',
        'error'
      ].indexOf(value) !== -1
    },
    default: 'some string'
  }
}
```

* v-for指定键值key
> 建议：使用“index + item[somekey]”，更好地区别了各个组件的key，高效的更新虚拟DOM

* v-if和v-for避免同时出现在同一元素上
> 建议：a.过滤一个列表中的某一项时，使用计算属性；b.避免渲染该隐藏的元素，v-if移到容器上

* 基础组件

特定的前缀，如dialog：DialogForm、DialogTable、DialogTableStudy

* 自闭合组件

单文件组件、字符串模板、JSX
``` html
  <!-- html -->
  <MyComponents />

  <!-- DOM模板 -->
  <my-components></my-components>
```

