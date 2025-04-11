---
title: vue组件通信——事件总线mitt
date: 2025-04-11 16:45:02
tags: [Vue3, mitt]
categories: [Vue3]
cover: https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20250411164619407.webp
---

> 理论上，事件总线可以实现任意组件之间的通信。 <mark>但是一般多用于兄弟组件之间的通信。</mark>

## 安装mitt

因为vue3原生没有提供事件总线这种方法，所以需要安装`mitt`来实现事件总线。

```shell
pnpm add mitt
```

然后在src目录下，创建一个文件夹utils：

![70d763465f1e4c5e9f0b141c796aca7b~tplv-73owjymdk6-jj-mark-v1_0_0_0_0_5o6Y6YeR5oqA5pyv56S-5Yy6IEAgTmljb2xhc0NhZ2U=_q75](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20250411164418017.webp)

```js
import mitt from "mitt"

const EventBus = mitt()

export default EventBus
```

`EventBus`有三个经常调用的方法：

![ed1a6844837f4519b2469aa53a40d927~tplv-73owjymdk6-jj-mark-v1_0_0_0_0_5o6Y6YeR5oqA5pyv56S-5Yy6IEAgTmljb2xhc0NhZ2U=_q75](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20250411164326803.webp)

1.  `emit`：触发事件
2.  `on`：监听事件
3.  `off`：清除事件

App.vue组件：

```html
<script setup>
import ChildComponent from "@/components/ChildComponent.vue"
import ChildComponent2 from "@/components/ChildComponent2.vue"
</script>

<template>
  <v-app>
    <ChildComponent />
    <ChildComponent2 />
  </v-app>
</template>
```

ChildComponent.vue组件：

```html
<script setup>
import {ref} from "vue"
import EventBus from "@/utils/emitter.js"

const child1Car = ref("法拉利")
</script>

<template>
  <div class="bg-purple h-50 w-75 ma-auto">
    <h1 class="text-center">我是子组件1</h1>
    <h2>子组件1的车：{{child1Car}}</h2>

    <!--用EventBus.emit触发事件-->
    <v-btn @click="EventBus.emit('sendCar',child1Car)" class="bg-blue ml-6">点我给兄弟送一台法拉利</v-btn>
  </div>
</template>
```

ChildComponent2.vue组件：

```html
<script setup>
import { ref,onUnmounted } from "vue"
import EventBus from "@/utils/emitter.js"

const child2Car = ref('')

// 监听事件
EventBus.on('sendCar', (value)=>{
  child2Car.value = value
})

//当组件卸载时，移除监听事件
onUnmounted(()=>{
  EventBus.off('sendCar')
})
</script>

<template>
  <div class="bg-blue h-50 w-75 ma-auto">
    <h1 class="text-center">我是子组件2</h1>
    <h2>组件1给我的车：{{child2Car}}</h2>
  </div>
</template>
```

效果图

![108ceac350b64cf988737589ee8d7cb3~tplv-73owjymdk6-jj-mark-v1_0_0_0_0_5o6Y6YeR5oqA5pyv56S-5Yy6IEAgTmljb2xhc0NhZ2U=_q75](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20250411164214628.webp)