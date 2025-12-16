---
title: 深入学习Vue
date: 2025-12-09 15:26:35
tags: ['Vue']
categories: VUE
cover: https://www4.bing.com//th?id=OHR.IceOtters_ZH-CN5393791969_1920x1080.jpg&rf=LaDigue_1920x1080.jpg&pid=hp
---

# 事件绑定 v-on

vue 同时支持两种形式的绑定

- 绑定方法引用（推荐）：

```html
<button v-on:click="handleClick">Click me</button>
```

- 绑定带括号的方法：

```html
<button v-on:click="addOne()">Add 1</button>
```

# `$event`

在 Vue.js 中，`$event`是一个特殊的变量，用于在事件处理函数中访问原生的 DOM 事件对象。当你在模板中绑定事件时，可以通过`$event`来获取事件对象，从而访问事件的各种属性和方法。

如果事件不需要传参数，那么也不需要显示的传`$event`，Vue 会自动将事件对象作为第一个参数传递给事件处理函数。但是推荐显示传递`$event`，这样代码更清晰。

```js
<input type="text" v-on:input="setName">

methods: {
  setName(event) {
    this.name = event.target.value
  },
}
```

如果事件函数需要传参数，那么就需要显示的传递`$event`，否则事件对象将无法传递给事件处理函数。

```js
<input type="text" v-on:input="setName($event, 'Tursun')">

methods: {
  setName(event, lastName) {
    this.name = event.target.value + ' ' + lastName
  },
}
```

# Event Modifiers(事件修饰符)

{% btn
 'https://vuejs.org/guide/essentials/event-handling.html#event-modifiers',
 'Vue官方文档-事件修饰符',
 far fa-hand-point-right,blue
%}

## Key Modifiers

可以通过键盘修饰符来监听特定的按键事件。

{% btn
 'https://vuejs.org/guide/essentials/event-handling.html#key-modifiers',
 'Vue官方文档-事件修饰符',
 far fa-hand-point-right,blue
%}

# `v-once`

`v-once`是 Vue.js 中的一个指令，用于将元素或组件渲染为只读的。使用`v-once`指令后，Vue 会在初始渲染时将该元素或组件的内容渲染到 DOM 中，但之后不会再进行任何更新，即使相关的数据发生变化。

```html
<button v-on:click="increment">Add</button>
<button v-on:click="decrement">Reduce</button>
<p v-once>Starting Counter: {{ counter }}</p>
<p>Counter: {{ counter }}</p>
```

```js
Vue.createApp({
  data() {
    return {
      counter: 0,
    }
  },
  methods: {
    increment() {
      this.counter++
    },
    decrement() {
      this.counter--
    },
  },
}).mount('#app')
```

Starting Counter: 0，即使点击按钮改变了`counter`的值，`v-once`绑定的内容也不会更新。

# `v-model` 修饰符

v-model 指令用于在表单元素和 Vue 实例的数据之间创建双向绑定。Vue 提供了一些修饰符，可以用来调整 v-model 的行为。

**手动事项 input 输入框的值双向绑定**：

```html
<input type="text" v-bind:value="name" v-on:input="updateName($event)" />
<p>{{ name }}</p>
<button v-on:click="resetName">resetName</button>
```

```js
const app = Vue.createApp({
  data() {
    return {
      name: '',
    }
  },

  methods: {
    updateName(event) {
      this.name = event.target.value
    },
    resetName() {
      this.name = ''
    },
  },
})

app.mount('#events')
```

但是 vue 给我们提供了一个语法糖:`v-model`：

```html
<input type="text" v-model="name" />
<p>{{ name }}</p>
<button v-on:click="resetName">resetName</button>
```

```js
const app = Vue.createApp({
  data() {
    return {
      name: '',
    }
  },

  methods: {
    resetName() {
      this.name = ''
    },
  },
})

app.mount('#events')
```

# vue 的页面渲染逻辑

Vue 使用虚拟 DOM（Virtual DOM）来优化页面渲染和更新的过程。虚拟 DOM 是一个轻量级的 JavaScript 对象，表示真实 DOM 的结构。当数据发生变化时，Vue 会创建一个新的虚拟 DOM 树，并将其与之前的虚拟 DOM 树进行比较（这个过程称为“diffing”）。通过比较两棵虚拟 DOM 树，Vue 能够确定哪些部分发生了变化，然后只更新那些实际需要改变的部分，从而提高性能。

{% note primary flat %}
Vue 在任意响应式数据变化时会触发渲染。
{% endnote %}

```html
<section id="events">
  <h2>Events in Action</h2>
  <input type="text" v-model="name" />
  <p>Full Name: {{ outputFullName() }}</p>
  <button v-on:click="resetName">resetName</button>
  <hr />
  <button v-on:click="function() {counter++}">Add 1</button>
  <p>{{ counter }}</p>
</section>
```

```js
const app = Vue.createApp({
  data() {
    return {
      name: '',
      counter: 0,
    }
  },

  methods: {
    // 只要有状态更新，这个方法就会重新执行
    outputFullName() {
      console.log('Running again...')
      if (this.name === '') return ''
      return this.name + ' ' + 'Tursun'
    },
    resetName() {
      this.name = ''
    },
  },
})

app.mount('#events')
```

> **原因分析**：
> 模板里用的是方法调用（outputFullName()），每次组件重新渲染都会执行该方法。Vue 在任意响应式数据（如 counter 或 name）变化时会触发渲染，因此每次点 > Add 时会重新执行并打印日志。
> **解决方案**：把需要缓存的逻辑改成 computed（基于依赖缓存），或者直接写到模板表达式里（不推荐）。

**直接写到模板里**:

```html
<!-- 只有当 name 变化时，模板会重新渲染 -->
<p>Full Name: {{ name + ' ' + 'Tursun' }}</p>
```

> 但是不推荐这样做，因为当模板变复杂时，表达式会变得难以维护。

# `computed` 计算属性

计算属性是基于它们的依赖进行缓存的。一个计算属性只有在它的相关响应式依赖发生变化时才会重新计算。这意味着如果你多次访问一个计算属性，而它的依赖没有变化，Vue 会直接返回之前计算的结果，而不会重新执行计算逻辑。

```html
<p>Full Name: {{ fullname }}</p>
```

```js
const app = Vue.createApp({
  data() {
    return {
      name: '',
      counter: 0,
    }
  },
  computed: {
    fullname() {
      console.log('Running again...')
      if (this.name === '') return ''
      return this.name + ' ' + 'Tursun'
    },
  },
  methods: {
    resetName() {
      this.name = ''
    },
  },
})

app.mount('#events')
```

> 所以，如果我们需要根据某些响应式数据计算出一个新的值，并且希望这个值在依赖没有变化时能够被缓存（不要在其它响应式数据更新的时候跟着更新）以提高性能，那么使用计算属性是一个非常好的选择。事件函数之类的就不适合用计算属性，因为事件函数通常是响应用户交互的，当用户触发这个事件的时候，我们希望它执行对应的函数逻辑。

# `watch` 侦听器

侦听器用于观察 Vue 实例上的数据变动。当被观察的数据发生变化时，侦听器会执行相应的回调函数。侦听器适用于需要在数据变化时执行异步操作或开销较大的操作的场景。

```html
<input type="text" v-model="name" />
<p>Full Name: {{ fullname }}</p>
```

```js
const app = Vue.createApp({
  data() {
    return {
      name: '',
      counter: 0,
      fullname: '',
    }
  },
  watch: {
    // 像监听哪个响应式数据，函数名就写成那个数据的
    name(newValue, oldValue) {
      if (newValue === '') this.fullname = ''
      else this.fullname = newValue + ' ' + 'Tursun'
    },
  },
  methods: {
    resetName() {
      this.name = ''
    },
  },
})

app.mount('#events')
```

{% note primary flat %}
注意，computed 属性也可以直接监听。
{% endnote %}

# `method`, 'computed', 'watch' 区别总结

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251212111615949.png)

# 控制样式

## style 绑定对象

```html
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px'}"></div>
```

## class 绑定对象

1. **绑定字符串：**

```html
<div :class="className"></div>

<!-- 根据条件设置 -->
<div :class="isActive ? 'active demo' : 'demo'"></div>
```

2. **绑定对象(很常用)：**

```html
<!-- key是类名，值是布尔值（true，false） -->
<div class="demo" :class="{ active: isActive, 'text-danger': hasError }"></div>
```

> 如果 class 如果很复杂的，很多的话推荐使用 computed 计算属性来返回一个对象。

3. **绑定数组：**

```html
<div :class="['demo', {active: isActive}]"></div>
```

# `v-for`

**渲染对象`object`**：

```html
<div v-for="(value, key, index) in object" :key="index">{{ index }}. {{ key }}: {{ value }}</div>
```

## v-for 为什么需要绑定 key 属性？

如果不绑定 key 属性，Vue 在更新列表时会使用“就地复用”的策略，“就地复用”策略是指：当数据发生变化时，Vue 不会实际删除 DOM 元素，而是把旧元素的内容（响应式数据）拿过来更新为刚刚删除的数据内容。

比如看个例子：

```html
<ul>
  <li v-for="(item, index) in items" :key="index" @click="removeItem(index)">
    <p>{{ item }}</p>
    <input type="text" />
  </li>
</ul>
```

```js
Vue.createApp({
  data() {
    return {
      items: [],
    }
  },

  methods: {
    removeItem(index) {
      this.items.splice(index, 1)
    },
  },
}).mount('#app')
```

在第二个 li 中的 input 中我输入一些信息之后，如果删除它前面的 li 元素，那么第二个 li 中的 input 内容会被第一个 li 中的 input 内容覆盖掉，因为 Vue 使用了“就地复用”策略，没有实际删除 DOM 元素，第一个 li 中的 input 是一种 dom 元素，而不是响应式数据，所以他会被复用覆盖掉第二个 li 中的 input。

那这个问题怎么解决呢？
`:key="index"`可以解决吗？
不可以，因为处在第一个位置的元素的 index 始终是 0，处在第二个位置的元素的 index 始终是 1，删除第一个元素之后，原来处在第二个位置的元素变成了第一个位置的元素，它的 index 变成了 0，所以 Vue 还是会复用这个 DOM 元素。

所以我们需要给 key 指定一个**唯一且不变**的值，比如数据项的 id 等等。

# refs

在 Vue.js 中，`refs` 是一个特殊的属性，用于直接访问组件实例或 DOM 元素。通过在模板中为元素或子组件添加 `ref` 属性，可以在 Vue 实例中通过 `this.$refs` 访问这些元素或组件。

```html
<input type="text" ref="myInput" /> <button v-on:click="focusInput">Focus Input</button>
```

```js
Vue.createApp({
  methods: {
    focusInput() {
      this.$refs.myInput.focus() // this.$refs.myInput相当于event.target
    },
  },
}).mount('#app')
```

{% note primary modern %}
**为什么使用这个 refs 呢？**
有时候我们需要直接操作 DOM 元素，比如设置焦点、获取元素的尺寸或位置等。使用 `refs` 可以方便地访问这些元素，而不需要通过复杂的选择器或事件传递。
比如上面的例子中，如果 vue 没有提供 refs，我们就需要通过`document.querySelector`来获取 input 元素，然后当点击按钮时给 input 设置焦点，反正很麻烦。
{% endnote %}

# 生命周期钩子函数

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251213195654878.png)

```js
const app = Vue.createApp({
  data() {
    return {
      message: '',
      currentUserInput: '',
    }
  },

  methods: {
    saveInput(event) {
      this.currentUserInput = event.target.value
    },
    setText() {
      this.message = this.currentUserInput
    },
  },

  beforeCreate() {
    console.log('before create')
  },
  created() {
    console.log('created')
  },
  beforeMount() {
    console.log('before mount')
  },
  mounted() {
    console.log('mounted')
  },
  beforeUpdate() {
    console.log('before update')
  },
  updated() {
    console.log('updated')
  },
  beforeUnmount() {
    console.log('before unmount')
  },
  unmounted() {
    console.log('unmounted')
  },
})

app.mount('#app')

// 手动销毁
setTimeout(function () {
  app.unmount()
}, 3000)
```

# component 组件基础

```js
const app = Vue.createApp()

/**
 * 给主应用程序注册一个组件
 * 组件名称：friend-contact
 * 这个组件跟主应用程序一样，有自己的数据和方法，反正主应用程序有的它都有
 * 推荐使用两个或者多个单词来命名组件，单词之间用连字符连接，防止和HTML元素冲突
 * template中只能使用自己的数据和方法，不能使用主应用程序的数据和方法,除非通过props传递数据
 *  */
app.component('friend-contact', {
  template: `
    <li>
      <h2>{{ friend.name}}</h2>
      <button @click="toggleDetails">{{detailsAreVisible ? 'Hide' : 'Show'}} Details</button>
      <ul v-if="detailsAreVisible">
        <li><strong>Phone:</strong> {{ friend.phone }}</li>
        <li><strong>Email:</strong> {{ friend.email }}</li>
      </ul>
      {{friends}} <!-- 这里会报错，因为friends是主应用程序的数据，组件中没有这个数据 -->
    </li>
  `,

  data() {
    return {
      friend: {
        id: 'manuel',
        name: 'Manuel Lorenz',
        phone: '123-4567',
        email: 'manuel@example.com',
      },
      detailsAreVisible: false,
    }
  },

  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible
    },
  },
})

app.mount('#app')
```

```html
<section id="app">
  <ul>
    <friend-contact></friend-contact>
    <friend-contact></friend-contact>
  </ul>
</section>
```

# Props 和 emits

## Props 校验

{% btn
 'https://vuejs.org/guide/components/props.html#prop-validation',
 'Vue官方文档-Props 校验',
 far fa-hand-point-right,blue
%}

```js
export default {
  props: {
    id: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    phone: {
      type: String,
      required: true,
    },
    email: {
      type: String,
      required: true,
    },
    isFavorite: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
}
```

## 自定义事件 emits

{% btn
 'https://vuejs.org/guide/components/events.html#events-validation',
 'Vue官方文档-自定义事件 emits',
 far fa-hand-point-right,blue
%}

```js
export default {
  // 这里显示的写子组件要触发的事件是主要为了让代码更清晰，可以不用写
  emits: {
    // 明确事件参数类型和校验, 如果校验成功返回 true, 失败返回 false
    'toggle-favorite': function (id) {
      if (id) {
        return true
      } else {
        console.warn('No ID provided!')
        return false
      }
    },
  },

  methods: {
    toggleFavorite() {
      // 触发自定义事件，并传递参数给父组件，如果没有传递参数，那么校验会失败
      this.$emit('toggle-favorite', this.id)
    },
  },
}
```

# provide / inject

{% btn
 'https://vuejs.org/guide/components/provide-inject.html',
 'Vue官方文档-provide / inject',
 far fa-hand-point-right,blue
%}

{% codeblock lang:js mark:32 %}

<template>
  <div>
    <active-element :topicTitle="activeTopic?.title" :text="activeTopic?.fullText"></active-element>
    <knowledge-base :topics="topics" @select-topic="activateTopic"></knowledge-base>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeTopic: null,
      topics: [
        {
          id: 'basics',
          title: 'The Basics',
          description: 'Core Vue basics you have to know',
          fullText:
            'Vue is a great framework and it has a couple of key concepts: Data binding, events, components and reactivity - that should tell you something!',
        },
        {
          id: 'components',
          title: 'Components',
          description: 'Components are a core concept for building Vue UIs and apps',
          fullText:
            'With components, you can split logic (and markup) into separate building blocks and then combine those building blocks (and re-use them) to build powerful user interfaces.',
        },
      ],
    }
  },

  provide() {
    return {
      topics: this.topics,
      // 引用methods中的方法activateTopic, 子组件可通过inject调用
      selectTopic: this.activateTopic,
    }
  },

  methods: {
    activateTopic(topicId) {
      this.activeTopic = this.topics.find(topic => topic.id === topicId)
    },
  },
}
</script>

{%endcodeblock%}

子组件使用数据：
{% codeblock lang:js mark:4,15 %}
<template>

  <ul>
    <knowledge-element
      v-for="topic in topics"
      :key="topic.id"
      :id="topic.id"
      :topic-name="topic.title"
      :description="topic.description"
    ></knowledge-element>
  </ul>
</template>

<script>
export default {
  inject: ['topics'],
}
</script>

{%endcodeblock%}

子组件调用父组件传递的方法：
{% codeblock lang:js mark:5,11 %}
<template>

  <li>
    <h3>{{ topicName }}</h3>
    <p>{{ description }}</p>
    <button @click="selectTopic(id)">Learn More</button>
  </li>
</template>

<script>
export default {
  inject: ['selectTopic'],
  props: ['id', 'topicName', 'description'],
}
</script>
{%endcodeblock%}

{% note warning flat %}
注意：
provide / inject 主要用于跨级组件通信，不建议在父子组件之间使用，父子组件之间推荐使用 props 和 emits。
{% endnote %}

# 组件导入

```js
import TheHeader from './components/TheHeader.vue'

export default {
  components: {
    TheHeader,
    // 也可以这样，但是更推荐上面的写法
    // 'the-header': TheHeader,
  },
}
```

```html
<template>
  <TheHeader></TheHeader>
  <!-- 也可以这样写 -->
  <!-- <the-header></the-header> -->
</template>
```

# 组件身上的attributes 和 listeners

{% btn
 'https://vuejs.org/guide/components/attrs.html#fallthrough-attributes',
 'Vue官方文档-组件身上的attributes',
 far fa-hand-point-right,blue
%}



# Slots 插槽

{% btn
 'https://vuejs.org/guide/components/slots.html#slots',
 'Vue官方文档-Slots 插槽',
 far fa-hand-point-right,blue
%}

# Dynamic Components(动态组件)

如果想根据某些条件动态切换组件，可以使用`<component>`标签和`:is`属性。
当然也可以使用`v-if`和`v-else-if`来切换组件，但是当组件比较多的时候，使用`<component>`标签会更简洁一些。

{% btn
 'https://vuejs.org/guide/essentials/component-basics.html#dynamic-components',
 'Vue官方文档-Dynamic Components(动态组件)',
 far fa-hand-point-right,blue
%}

如果切换组件时想要保持组件的数据，可以使用`keep-alive`包裹动态组件。

{% btn
 'https://vuejs.org/guide/built-ins/keep-alive.html#keepalive',
 'Vue官方文档-Keep Alive(保持组件状态)',
 far fa-hand-point-right,blue
%}

# Teleport 传送门

`teleport` 允许你将组件的内容渲染到 DOM 树中的另一个位置，而不是组件本身所在的位置。

{% btn
 'https://vuejs.org/guide/built-ins/teleport.html#teleport',
 'Vue官方文档-Teleport 传送门',
 far fa-hand-point-right,blue
%}

vue官网是这样说的：
{% note warning flat %}
**TIP**

The teleport to target must be already in the DOM when the `<Teleport>` component is mounted. Ideally, this should be an element outside the entire Vue application. If targeting another element rendered by Vue, you need to make sure that element is mounted before the `<Teleport>`.
{% endnote %}

所以：`to="body"` 永远是最稳妥的，因为 body 一定在 Vue 挂载前就存在。

# 最佳实践

{% btn
 'https://vuejs.org/style-guide/',
 'Vue官方文档-最佳实践',
 far fa-hand-point-right,blue
%}

{% note warning flat %}
注意：
这个最佳实践官方已标记为`outdated`，可能对于composition API不适用。
{% endnote %}