---
title: Vue3 Props and Emits
date: 2025-04-10 17:34:23
tags: [Vue3, Vue]
categories: Vue3
cover: https://cn.bing.com//th?id=OHR.LittleFoxes_ZH-CN8622806156_1920x1080.jpg&rf=LaDigue_1920x1080.jpg&pid=hp
---

## 什么是props

props（properties）就是父组件给子组件传递的数据。

## 怎么接受props

typescript中，我们需要先声明一个interface，确定父组件传递属性有哪些。

```typescript
<script setup lang="ts">
import {defineProps} from 'vue'
    
interface Props {
  name: string
  age?: number
}
    
const props = defineProps<Props>()
</script>
```

## props赋默认值

用interface定义的props可以通过解构的方式赋默认值。

{% note warning modern %}
**注意**
在 Vue 3.4 及以下版本中，直接解构 `props` 会失去响应式。   
Vue 3.5+ 会自动将解构变量转换为 `props.xxx`，但推荐使用 `withDefaults` 以保持一致性。
{% endnote %}

```typescript
<script setup lang="ts">
import {defineProps} from 'vue'
    
interface Props {
  name: string
  age?: number
}
    
const {name = 'akbar', age = 18} = defineProps<Props>()
</script>
```

{% note warning modern %}
**注意**
上面这种解构的方法虽然可行，但是官方并不推荐。
官方更推荐使用**withDefaults**
{%  endnote %}

```typescript
<script setup lang="ts">
import {defineProps} from 'vue'
    
interface Props {
  name: string
  age?: number
}
    
const props = withDefaults(defineProps<Props>(), {
    name: 'akbar',
    age: 23,
})
</script>
```

需要注意的是，如果是引用类型并且是可选的，用`withDefaults`赋默认值时，为了避免意外修改和外部副作用，应该使用函数包装。

比如像下面这样：

```typescript
<script lang="ts" setup>
import {defineProps, withDefaults} from 'vue'
    
interface Props {
  msg?: string
  labels?: string[]
}

const props = withDefaults(defineProps<Props>(), {
  msg: 'hello',
  // 注意这里的函数包装
  labels: () => ['one', 'two']
})
</script>
```

## emits

`emit`用于声明由组件触发的自定义事件。

触发自定义事件，格式：`emit(eventName, ...args)`。

**子组件：**

```typescript
<script lang="ts" setup>
import { defineEmits } from 'vue'

// 声明由组件触发的自定义事件
const emits = defineEmits(['cardClick'])
</script>

<template>
  <button @click="$emit('cardClick')">Click me!</button>
</template>
```

如果自定义事件在模板中（template）触发用`$emit(eventName, ...args)`。

如果在script中触发就用`emit(eventName, ...args)`触发即可。

**父组件：**

```typescript
<script lang="ts" setup>
import Card from './components/Card.vue'

const handleClick = () => {
  console.log('Card clicked')
}
</script>

<template>
  <!--父组件需要监听子组件出发的card-click事件，并执行相应的处理函数-->
  <Card @card-click="handleClick" />
</template>
```

## emit自定义事件携带参数

自定义事件携带参数很简单。

**子组件：**

```typescript
<script lang="ts" setup>
import { defineProps, defineEmits } from 'vue'

interface Props {
  title?: string
}

const { title = 'This is my card title' } = defineProps<Props>()
// 声明由组件触发的自定义事件
const emits = defineEmits(['cardClick'])
</script>

<template>
  <button @click="$emit('cardClick', title)">Click me!</button>
</template>
```

**父组件：**

```typescript
<script lang="ts" setup>
import Card from './components/Card.vue'

const handleClick = (value: string) => {
  console.log(value)
}
</script>

<template>
  <Card @card-click="handleClick" />
</template>
```