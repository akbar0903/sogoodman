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

- `created`：在实例创建完成后被调用，此时数据和事件配置已经完成，但 DOM 还未挂载。
- `mounted`：在实例挂载到 DOM 后被调用，此时可以访问和操作 DOM 元素。

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

# 组件身上的 attributes 和 listeners

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

vue 官网是这样说的：
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
这个最佳实践官方已标记为`outdated`，可能对于 composition API 不适用。
{% endnote %}

# Form Controls

## Form Bindings

{% btn
 'https://vuejs.org/guide/essentials/forms.html#form-input-bindings',
 'Vue官方文档-Form Bindings',
 far fa-hand-point-right,blue
%}

## Component v-model

{% btn
 'https://vuejs.org/guide/components/v-model.html#component-v-model',
 'Vue官方文档-Component v-model',
 far fa-hand-point-right,blue
%}

> 我们发现一个规律，自定义组件中使用v-model，响应式数据一般都在父组件中定义，然后通过prop传递给子组件，子组件通过事件把数据传递回父组件。

**下面介绍一个坑：**

父组件：
{% codeblock lang:js mark:28 %}
<script>
  import RatingControl from './RatingControl.vue'

  export default {
    components: {
      RatingControl,
    },

    data() {
      return {
        rating: null,
      }
    },

    methods: {
      submitForm() {
        console.log('rating:', this.rating)
        this.rating = null
      },
    },
  }
</script>

<template>
  <form class="demo-form" @submit.prevent="submitForm">
    <div class="field">
      <label class="label-text">Rate our website</label>
      <RatingControl :model-value="rating" @update:model-value="rating = $event" />
    </div>

    <div class="actions">
      <button type="submit" class="btn-save">Save Data</button>
    </div>
  </form>
</template>

<!-- 样式省略 -->
{%endcodeblock%}

子组件：
{% codeblock lang:js mark:8 %}
<script>
export default {
  props: ['modelValue'],
  emits: ['update:modelValue'],

  data() {
    return {
      activeOption: this.modelValue, // 组件创建的时候只执行一次这个赋值操作
    }
  },

  methods: {
    activate(option) {
      this.activeOption = option
      this.$emit('update:modelValue', option)
    }
  }
}
</script>

<template>
  <ul>
    <li>
      <button type="button" @click="activate('poor')" :class="{ active: activeOption === 'poor' }">
        Poor
      </button>
    </li>
    <li>
      <button
        type="button"
        @click="activate('average')"
        :class="{ active: activeOption === 'average' }"
      >
        Average
      </button>
    </li>
    <li>
      <button
        type="button"
        @click="activate('great')"
        :class="{ active: activeOption === 'great' }"
      >
        Great
      </button>
    </li>
  </ul>
</template>
{%endcodeblock%}

现在我遇到的问题是：为什么我点击提交按钮提交的时候，子组件的`activeOption`不会被清零？按理来说：当按下提交按钮的时候父组件把一个清零的prop，也就是`:model-value="rating`作为prop传递给子组件，然后子组件拿着这个值赋值给`activeOption`，`activeOption`应该被清零才对啊？

**原因分析**：
在子组件中，`activeOption` 只在组件创建时被初始化为 `this.modelValue` 的值。要注意，每个vue组件都有自己独立的响应式数据（data（））返回的数据，他不会随着某个prop的变化而自动变化。

**解决办法：**
- 在子组件中使用`watch`监听`modelValue`的变化，然后在变化时更新`activeOption`。{% label 不推荐 orange %}
- 直接在子组件的模板中使用`modelValue`，而不是在data中创建一个新的`activeOption`变量。{% label 推荐 green %}

**下面用推荐的接办法来解决：**
父组件：
{% codeblock lang:js mark:28-29 %}
<script>
  import RatingControl from './RatingControl.vue'

  export default {
    components: {
      RatingControl,
    },

    data() {
      return {
        rating: null,
      }
    },

    methods: {
      submitForm() {
        console.log('rating:', this.rating)
        this.rating = null
      },
    },
  }
</script>

<template>
  <form class="demo-form" @submit.prevent="submitForm">
    <div class="field">
      <label class="label-text">Rate our website</label>
      <!-- <RatingControl :model-value="rating" @update:model-value="rating = $event" /> -->
      <RatingControl v-model="rating" />    <!-- 推荐使用v-model语法糖 -->
    </div>

    <div class="actions">
      <button type="submit" class="btn-save">Save Data</button>
    </div>
  </form>
</template>
{%endcodeblock%}

子组件：
{% codeblock lang:js mark:3-4,8,17 %}
<script>
export default {
  props: ['modelValue'],
  emits: ['update:modelValue'],

  methods: {
    activate(option) {
      this.$emit('update:modelValue', option)
    }
  }
}
</script>

<template>
  <ul>
    <li>
      <button type="button" @click="activate('poor')" :class="{ active: modelValue === 'poor' }">
        Poor
      </button>
    </li>
    <li>
      <button
        type="button"
        @click="activate('average')"
        :class="{ active: modelValue === 'average' }"
      >
        Average
      </button>
    </li>
    <li>
      <button
        type="button"
        @click="activate('great')"
        :class="{ active: modelValue === 'great' }"
      >
        Great
      </button>
    </li>
  </ul>
</template>
{%endcodeblock%}

**下面在看一个示例代码：**

父组件：
{% codeblock lang:html mark:13 %}
<script>
import { computed, reactive } from 'vue'
import CoachFilter from '../../components/coaches/CoachFilter.vue'

export default {
  components: {
    CoachFilter,
  },

  setup() {
    const coachesStore = userCoachesStore()

    const activeFilters = reactive({
      frontend: false,
      backend: false,
      career: false,
    })

    const filteredCoaches = computed(function () {
      const filters = activeFilters

      return coachesStore.coachesList.filter(coach => {
        if (filters.frontend && !coach.areas.includes('frontend')) return false
        if (filters.backend && !coach.areas.includes('backend')) return false
        if (filters.career && !coach.areas.includes('career')) return false

        return true
      })
    })

    return {
      coachesStore,
      activeFilters,
      filteredCoaches,
    }
  },
}
</script>

<template>
  <section>
    <coach-filter :modelValue="activeFilters" @update:modelValue="activeFilters = $event" />
    {{activeFilters}}
  </section>
</template>
{%endcodeblock%}

> 这段代码中的`{{activeFilters}}`不会更新的，发现问题所在了吗？
> 
> 这段代码中响应数据activeFilters用的是`reactive`，然后用`@update:modelValue="activeFilters = $event"`完整替换了这个响应式对象，所以activeFilters失去了响应式特性，导致模板中的`{{activeFilters}}`不会更新。
> 解决办法：
> - 不要完整替换响应式对象，而是更新对象的属性。可以采用对象展开运算符，或者Object.assign()等方式。
> - 直接使用`ref`来定义activeFilters。

为什么ref可以呢？

| 机制  |	reactive |	ref |
|-------|----------|-----|
| 返回值 | Proxy 代理对象 | 响应式包装对象 |
| 重新赋值 | 变量指向新对象，原代理被丢弃 | .value 是响应式追踪点 |
| 结果 | ❌ 新对象无响应式 | ✅ 触发响应式更新 |

# 表单校验

可以利用`blur`事件来完成对表单的校验：

```html
<div class="field" :class="{ invalid: usernameValidity === 'invalid' }">
  <label class="label-text" for="name">Your Name</label>
  <input
    id="name"
    type="text"
    name="name"
    class="input"
    placeholder="Enter your name"
    v-model.trim="username"
    @blur="validateInput"
  />
  <p v-if="usernameValidity === 'invalid'">Please enter your name.</p>
</div>

<style>
  .field {
    display: block;
  }

  .label-text {
    display: block;
    font-weight: 600;
    margin-bottom: 6px;
    color: #111827;
  }

  .input {
    width: 100%;
    padding: 9px 10px;
    border: 1px solid #d1d5db;
    border-radius: 4px;
    font-size: 14px;
    background: #fff;
    color: #0b1220;
    box-sizing: border-box;
  }

  /* 校验失败样式 */
  .field.invalid .input {
    border-color: red;
  }

  .field.invalid p {
    margin: 4px 0 0;
    font-size: 13px;
    color: red;
  }
</style>
```

```js
export default {
  data() {
    return {
      username: '',
      usernameValidity: 'pending',
    }
  },

  methods: {
    validateInput() {
      if (this.username === '') {
        this.usernameValidity = 'invalid'
      } else {
        this.usernameValidity = 'valid'
      }
    },
  },
}
```

# Vue-Router

```js
import { createApp } from 'vue'
import App from './App.vue'
import TeamsList from './components/teams/TeamsList.vue'
import UsersList from './components/users/UsersList.vue'
import { createRouter, createWebHistory } from 'vue-router'

const router = createRouter({
  history: createWebHistory(),
  routes: [
    {
      path: '/teams',
      name: 'Teams'
      component: TeamsList,
    },
    {
      path: '/users',
      name: 'Users'
      component: UsersList,
    },
  ],
})


const app = createApp(App)

app.use(router)

app.mount('#app')
```

history有三种模式：
- createWebHistory()：HTML5 History 模式，URL 中没有 # 号，适合现代浏览器。
- createWebHashHistory()：Hash 模式，URL 中有 # 号，适合不支持 HTML5 History API 的浏览器。
- createMemoryHistory()：内存模式，主要用于服务器端渲染（SSR）。

## 路由出口Router-View



## 声明式导航router-link

`router-link`会渲染成`<a>`标签。

### path导航

```html
<!-- 根据path导航 -->
<router-link to="/teams">Teams</router-link>
```

### name导航

```html
<!-- 根据name导航 -->
<router-link :to="{ name: 'Teams' }">Teams</router-link>
```

### 修改激活状态样式

激活状态的路由链接会自动添加`router-link-active`和`router-link-exact-active`类名，可以通过 CSS 来定义这些类名的样式。
- `router-link-active`：当路由部分匹配时应用该类名。有嵌套路由时会应用该类名。
- `router-link-exact-active`：当路由完全匹配时应用该类名。

```css
a:hover,
a:active,
a.router-link-active {
  color: #f1a80a;
}
```

如果想修改默认的类名，请参考官方文档：

{% btn
 'https://router.vuejs.org/guide/essentials/active-links.html#Configuring-the-classes',
 'Vue-Router官方文档-修改激活状态样式',
 far fa-hand-point-right,blue
%}

## 编程式导航

{% btn
 'https://router.vuejs.org/guide/essentials/navigation.html',
 'Vue-Router官方文档-编程式导航',
 far fa-hand-point-right,blue
%}

一旦我们把router挂到vue实例上，比如：`app.use(router)`，我们就可以全局拿到`this.$router`和`this.$route`。

### $router

- `this.$router`：路由器实例，可以用来编程式导航。

```js
this.$router.push('/teams')           // 根据路径导航
this.$router.push({ name: 'Teams' }) // 根据路由名称导航
```

### $route

- `this.$route`：当前路由的信息对象，可以用来访问当前路由的参数、查询字符串等信息。

```js
// 路由url是这样的：/users/:userId

/**
 * 获取路由参数userId
 * 建议在created钩子函数中获取路由参数，因为此时路由信息已经准备好了
 */
this.$route.params.userId 
```

{% note warning flat %}
**注意：**
组合式api中使用路由器时，需要使用`useRouter`和`useRoute`来获取路由器实例和当前路由信息。因为组合式api中没有`this`上下文。
但是在模板`<template>`中可以使用`$router`和`$route`，因为模板中有上下文。
{% endnote %}

### 把url参数作为props传递给组件

```js
    {
      path: '/teams/:teamId',
      component: TeamMembers,
      props: true,
    },
```

然后子组件可以直接通过props接收`teamId`。

## 重定向和Alias

{% btn
 'https://router.vuejs.org/guide/essentials/redirect-and-alias.html#Redirect-and-Alias',
 'Vue-Router官方文档-重定向和Alias',
 far fa-hand-point-right,blue
%}

## 404或者未知路由

```js
    {
      // 意思就是匹配所有(/)后面的内容，这里不一定要写notFound，可以是任意名称
      // 注意，这个路由一定要放在最后面，因为路由是按照顺序进行匹配的
      path: '/:notFound(.*)',
      redirect: '/teams', 
      // 或者
      // component: NotFoundComponent,
    },
```

## Scroll Behavior

{% btn
 'https://router.vuejs.org/guide/advanced/scroll-behavior.html#Scroll-Behavior',
 'Vue-Router官方文档-Scroll Behavior',
 far fa-hand-point-right,blue
%}

我们经常使用的应该是这个：
```js
const router = createRouter({
  scrollBehavior(to, from, savedPosition) {
    if (savedPosition) {
      return savedPosition
    } else {
      return { top: 0 }
    }
  },
})
```

## Navigation Guards

{% btn
 'https://router.vuejs.org/guide/advanced/navigation-guards.html',
 'Vue-Router官方文档-Navigation Guards',
 far fa-hand-point-right,blue
%}

- `to`：即将要进入的目标路由对象。
- `from`：当前导航正要离开的路由对象。
- `next`：一个函数，必须调用该函数来 resolve 这个钩子。

看个例子：
```js
// GOOD
router.beforeEach((to, from, next) => {
  if (to.name !== 'Login' && !isAuthenticated) next({ name: 'Login' })
  else next()
})
```
上面的代码的意思是：如果用户没有认证，并且要去的路由不是登录页，那么就重定向到登录页，否则放行。

# transition

为什么要用vue提供的transition组件呢？我们使用css实现动画不行吗？

我们使用vue的transition组件是因为：
css动画只能在元素在DOM中时起作用，而vue的transition组件可以在元素进入和离开DOM时触发动画。
比如一个模态框为例，如果用css动画实现，当模态框出现的时候可以实现动画，但是关闭模态框的时候，模态框会立即从DOM中移除，动画就无法实现了，而使用vue的transition组件可以在模态框离开DOM之前先执行动画，然后再移除DOM。

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251218144215624.png)

transition组件默认有这些类名：

**进入：**
- `v-enter-from`：元素进入时的起始状态，
- `v-enter-active`：元素进入时的过渡状态，
- `v-enter-to`：元素进入时的结束状态，

**离开：**
- `v-leave-from`：元素离开时的起始状态，
- `v-leave-active`：元素离开时的过渡状态，
- `v-leave-to`：元素离开时的结束状态，

{% note warning flat %}
注意：

transition组件只能有一个root组件。
如果需要有两个组件，要保证在DOM上不能同时存在这两个组件，可以使用`mode`属性来控制组件的切换顺序。v-if来控制组件的显示和隐藏。
{% endnote %}

# Composition API

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251220164229554.png)

composition api 中不能拿到`this`，因为`setup`函数是在组件实例创建之前执行的，所以没有`this`上下文。

# setup 函数

```html
<script>
import { ref } from 'vue'

export default {
  setup() {
    const username = ref('Akbar Tursun')
    const age = ref(22)

    setTimeout(function () {
      username.value = 'Changed Name'
      age.value = 30
    }, 2000)

    return {
      username,
      age,
    }
  },
}
</script>

<template>
  <h1>{{ username }}</h1>
  <h1>{{ age }}</h1>
</template>
```

## setup 语法糖

{% btn
 'https://vuejs.org/guide/essentials/reactivity-fundamentals.html#script-setup',
 'Vue官方文档-setup 语法糖',
 far fa-hand-point-right,blue
 %}

# Ref 和 Reactive

ref 和 reactive 都是 Vue 3 中用于创建响应式数据的 API，但它们有一些关键的区别：
- `ref`：用于创建一个包含单个值的响应式引用。它适用于基本数据类型（如字符串、数字、布尔值）以及对象和数组。当你使用 ref 创建一个响应式引用时，你需要通过 `.value` 属性来访问和修改其值。
- `reactive`：用于创建一个响应式对象。它适用于复杂的数据结构，如对象和数组。使用 reactive 创建的对象会递归地将其属性转换为响应式的，因此你可以直接访问和修改对象的属性，而不需要使用 `.value`。

## ref

{% btn
 'https://vuejs.org/guide/essentials/reactivity-fundamentals.html#why-refs',
 'Vue官方文档-ref',
 far fa-hand-point-right,blue
 %}

## reactive

{% btn
 'https://vuejs.org/guide/essentials/reactivity-fundamentals.html#reactive',
 'Vue官方文档-ref',
 far fa-hand-point-right,blue
 %}

## 疑点

```js
import { ref } from 'vue'

export default {
  setup() {
    const name = ref('Alice')  // 创建一个ref
    const age = ref(25)
    
    return {
      name,  // ✅ 保持响应式
      age,   // ✅ 保持响应式
    }
  }
}
```
为什么 ref能保持响应性，而 reactive的属性会丢失？

**ref**：

```js
// ref 创建的是一个包装对象：
const name = ref('Alice')
console.log(name) // RefImpl { value: 'Alice' }

// 返回的是这个 Ref 对象本身
return { name } // ✅ 返回的是整个 RefImpl 对象
```

**reactive**：

```js
const user = reactive({ name: 'Alice' })

// 这里 user.name 是字符串 'Alice'，不是响应式对象
console.log(user.name) // 'Alice'（普通字符串）

// 返回的是字符串值，不是响应式对象
return { name: user.name } // ❌ 返回的是普通字符串
```

**关键记忆点**：
ref返回的是"箱子"，reactive返回的是"箱子里的东西"
ref→ 返回整个箱子（响应式）
reactive.property→ 只拿出箱子里的东西（不响应）

# composition api methods

```html
<script>
import { ref } from 'vue'

export default {
  setup: function () {
    const username = ref('John Doe')
    const age = ref(18)

    // 函数里面定义方法是没有问题的
    const changeAge = function () {
      age.value += 1
    }

    return {
      username,
      age,
      changeAge,
    }
  },
}
</script>

<template>
  <h1>{{ username }}</h1>
  <h1>{{ age }}</h1>
  <button @click="changeAge">change age</button>
</template>
```

# composition api computed

```html
<script>
import { ref, computed } from 'vue'

export default {
  setup: function () {
    const firstName = ref('')
    const lastName = ref('')

    const setFirstName = function (event) {
      firstName.value = event.target.value
    }

    const setLastName = function (event) {
      lastName.value = event.target.value
    }

    // fullName 也是一种ref，但是它是一个只读的ref
    const fullName = computed(function () {
      return firstName.value + ' ' + lastName.value
    })

    return {
      firstName,
      lastName,
      setFirstName,
      setLastName,
      fullName,
    }
  },
}
</script>

<template>
  <div>
    <input type="text" placeholder="First Name" @input="setFirstName" />
    <input type="text" placeholder="Last Name" @input="setLastName" />
  </div>
  <div>
    <h2>Full Name: {{ fullName }}</h2>
  </div>
</template>
```

# composition api watch

```html
<script>
import { ref, watch } from 'vue'

export default {
  setup: function () {
    const age = ref(23)

    const changeAge = function () {
      age.value += 1
    }

    watch(age, function (newVal, oldVal) {
      console.log('Age changed from', oldVal, 'to', newVal)
    })

    return { age, changeAge }
  },
}
</script>

<template>
  <div>
    <button @click="changeAge">change Age</button>
  </div>
  <h2>{{ age }}</h2>
</template>
```

如果需要watch多个响应式数据，可以传递一个数组作为第一个参数：

```js
watch([firstName, lastName], function ([newFirstName, newLastName], [oldFirstName, oldLastName]) {
  console.log('First Name changed from', oldFirstName, 'to', newFirstName)
  console.log('Last Name changed from', oldLastName, 'to', newLastName)
})
```

{% note primary flat %}
根据vue官方文档，watch的第一个参数可以是以下几种类型：
- 响应式ref
- 响应式reactive 对象
- getter function
{% endnote %}

**什么是getter function：**
- 普通JavaScript函数
- 返回值是我们要监听的数据
- 每次执行都能获取最新值

```js
// Vue中的"getter" - 实际上是普通函数
() => obj.count
() => props.user.name
() => x.value + y.value
```

监听reactive对象属性的时候注意：
```javascript
const obj = reactive({ count: 0 })

// this won't work because we are passing a number to watch()
watch(obj.count, (count) => {
  console.log(`Count is: ${count}`)
})
```

Instead, use a getter:
```js
// instead, use a getter:
watch(
  () => obj.count,
  (count) => {
    console.log(`Count is: ${count}`)
  }
)
```

# Refs

```html
<script>
import { ref } from 'vue'

export default {
  setup: function () {
    // 初始化的时候是null，因为还没有绑定到真实的DOM元素上
    const nameInput = ref(null)
    const name = ref('akbar')

    const focusOnInput = function () {
      // 跟this.$refs.nameInput.focus()效果一样
      nameInput.value.focus()
    }

    return {
      name,
      // 这里暴露出去，然后在模板中通过ref绑定
      nameInput,
      focusOnInput,
    }
  },
}
</script>

<template>
  <div>
    <input type="text" ref="nameInput" />
  </div>
  <div>
    <button @click="focusOnInput">聚焦nameInput</button>
  </div>
</template>
```

# Props 和 Emits

## Props

**第一种方式**
```html
<script>
export default {
  props: ['username', 'age'],

  setup() {
    return {
    }
  },
}
</script>

<template>
  <h2>{{ username }}</h2>
  <h2>{{ age }}</h2>
</template>
```
是的，不要觉得奇怪，props可以直接在模板中使用，因为模板有上下文。

**第二种方式**
```html
<script>
export default {
  props: {
    username: {
      type: String,
      required: true,
    },
    age: {
      type: Number,
      required: true,
    },
  },

  setup(props) {
    // 这里的props就是上面定义的props对象
    console.log(props.username)
    console.log(props.age)

    return {
    }
  },
}
</script>

```

**第三种方法是**使用`setup`语法糖：
```html
<script setup>
defineProps({
  username: {
    type: String,
    required: true,
  },
  age: {
    type: Number,
    required: true,
  },
})
</script>
```

{% note warning flat %}

注意：

解构props失去响应式的行为在不同Vue版本中表现不同：

1. **Vue 3.5之前**：解构props会失去响应性
2. **Vue 3.5之后**：编译器自动转换解构变量为props.变量名，保持响应性

监听规则：
- ✅ 可以监听：props.user
- ✅ 可以监听：props.anyPropName  
- ✅ 可以监听：解构的变量（Vue 3.5+）

{% endnote %}

正确示例：
```js
// Vue 3.5+ - 可以监听解构的变量
const { foo } = defineProps(['foo'])
watch(() => foo, /* ... */) // 正确

// 也可以监听原始prop
const { foo } = defineProps(['foo'])
watch(() => props.foo, /* ... */) // 正确

// 或者直接监听props属性
const props = defineProps(['foo'])
watch(() => props.foo, /* ... */) // 正确

// 错误示例（不要这样写）
watch(foo, /* ... */) // ❌ 错误：应该包装成函数
```


## Emits

**第一种方式**
```html
<script>
export default {
  emits: ['custom-event'],
  setup(props, context) {
    const triggerEvent = function () {
      context.emit('custom-event', 'Hello from child component')
    }

    return {
      triggerEvent,
    }
  },
}
</script>

<template>
  <button @click="triggerEvent">Trigger Custom Event</button>
</template>
```

**第二种方式**使用`setup`语法糖：
```html
<script setup>
defineEmits(['custom-event'])
const triggerEvent = function () {
  emit('custom-event', 'Hello from child component')
}
</script>

<template>
  <button @click="triggerEvent">Trigger Custom Event</button>
</template>
```

# Provide / Inject

**Provide**:

```html
<script>
import { provide, ref } from 'vue'

export default {
  setup() {
    const topics = ref([
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
    ])

    const activateTopic = function (topicId) {
      console.log('Activating topic:', topicId)
    }

    provide('topics', topics)
    provide('selectTopic', activateTopic)
  },
}
</script>
```

**Inject**:

```html
<script>
import { inject } from 'vue'

export default {
  setup() {
    const topics = inject('topics')
    const selectTopic = inject('selectTopic')

    return {
      topics,
      selectTopic,
    }
  },
}

</script>
```

# Lifecycle Hooks

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251220203837996.png)

需要注意的是，在composition api中，不需要``beforeCreate`和`created`钩子，因为`setup`函数本身就相当于这两个钩子的结合体。
