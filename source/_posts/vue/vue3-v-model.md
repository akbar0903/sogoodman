---
title: Vue3 v-model
date: 2025-04-11 16:22:50
tags: [Vue3, Vue]
categories: Vue3
cover: https://www4.bing.com//th?id=OHR.PenguinLove_ZH-CN9124008164_1920x1080.jpg&rf=LaDigue_1920x1080.jpg&pid=hp
---



刚开始学习vue3的时候，理解起来最难的是v-model，虽然我们直接可以使用官方封装好的`defineModel()宏`，但是不了解底层怎么实现的，总感觉心里不踏实。

## v-model可以干什么

我们都知道，`v-model` 用于实现数据的双向绑定。

## 底层的实现方式

下面写一段代码示例，实现组件之间数据的双向绑定。

**子组件：**

```ts
<script lang="ts" setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps(['modelValue'])
const emits = defineEmits(['update:modelValue'])
</script>

<template>
  <input
    :value="props.modelValue"
    @input="$emit('update:modelValue', ($event.target as HTMLInputElement).value)"
  />
  <p>子组件：{{ props.modelValue }}</p>
</template>
```

>   上面的代码很好理解，首先把父组件传递的modelValue的值给input，然后当input标签的输入框输入发生变换的时候，子组件触发自定义事件`update:modelValue`。



**父组件：**

```ts
<script lang="ts" setup>
import { ref } from 'vue';
import Card from './components/Card.vue'

const text = ref('Hello World')
</script>

<template>
  <Card :model-value="text" @update:model-value="text = $event" />
  <p>父组件：{{ text }}</p>
</template>
```

>   上面的代码中，首先父组件给子组件传递了一个props text，然后父组件还要监听由子组件触发的事件`@update:model-value`。
>
>   我们看到子组件在触发自定义事件的时候是这样出发的`$emit('update:modelValue', ($event.target as HTMLInputElement).value)`，第一个参数是`eventName`，第二个是自定义事件携带的参数`args`，所以我们监听由子组件触发的自定义事件`@update:model-value`的时候需可以拿到这个参数：`@update:model-value="text = $event"`。

官方文档中父组件中拿到的这个参数是这样写的`text = $event`，但是我感觉这样很容易混淆，因为子组件中$event是事件对象，而父组件中就变成了时间参数，这个并不好，当然这只是参数而已，用什么无所谓。

我觉得最好的写法是这样的：

```ts
<script lang="ts" setup>
import { ref } from 'vue';
import Card from './components/Card.vue'

const text = ref('Hello World')
</script>

<template>
  <Card :model-value="text" @update:model-value="(value: string) => text = value" />
  <p>父组件：{{ text }}</p>
</template>
```

>   `(value: string) => text = value"`
>
>   Vue 的设计是为了简洁，但箭头函数确实更明确。

## defineModel()

原生写法有时候显得比较啰嗦，我们可以使用官方提供的`defineModel()` 。

从 Vue 3.4 开始，推荐的实现方式是使用 `defineModel()` 宏：

**子组件：**

```ts
<script lang="ts" setup>
import { defineModel } from 'vue'

const model = defineModel()
</script>

<template>
  <input v-model="model" />
  <p>子组件：{{ model }}</p>
</template>
```

**父组件：**

```ts
<script lang="ts" setup>
import { ref } from 'vue';
import Card from './components/Card.vue'

const text = ref('Hello World')
</script>

<template>
  <Card v-model="text" />
  <p>父组件：{{ text }}</p>
</template>
```

`defineModel()` 返回的值是一个 ref。它可以像其他 ref 一样被访问以及修改，不过它能起到在父组件和当前变量之间的双向绑定的作用：

*   它的 `.value` 和父组件的 `v-model` 的值同步；
*   当它被子组件变更了，会触发父组件绑定的值一起更新。