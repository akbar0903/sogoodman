---
title: 优秀项目学习——nova-admin
date: 2025-04-16 20:13:04
tags: ['Vue3']
categories: '优秀项目学习'
cover: https://www4.bing.com//th?id=OHR.PolarCub_ZH-CN1179361319_1920x1080.jpg&rf=LaDigue_1920x1080.jpg&pid=hp
---

# 图标icon处理
> 我使用的是`xicons`，选择`antd`:
> 官网：https://xicons.org/#/
> 使用方法（访问GitHub仓库）：https://github.com/07akioni/xicons

# 登录注册页面

## 父组件
这个父组件包裹`Login, Register, ResetPwd`等组件
{% codeblock lang:ts 父组件index.vue mark:18,59-61 %}
<script lang="ts" setup>
import { ref, type Ref } from 'vue'
import { NEl, NH3 } from 'naive-ui'
import Login from './components/Login/index.vue'
import Register from './components/Register/index.vue'
import ResetPwd from './components/ResetPwd/index.vue'

const formType: Ref<'login' | 'register' | 'resetPwd'> = ref('login')
const formComponent = {
  login: Login,
  register: Register,
  resetPwd: ResetPwd,
}
</script>

<template>
  <NEl
    class="w-full h-full flex items-center justify-center"
    style="background-color: var(--body-color)"
  >
    <!-- 主题切换按钮 -->
    <div class="fixed top-10 right-10 text-lg">主题切换</div>

    <!-- 卡片 -->
    <NEl
      class="p-8 h-full w-full sm:w-[450px] sm:h-[700px]"
      style="background-color: var(--card-color); box-shadow: var(--box-shadow-1)"
    >
      <div class="w-full flex flex-col items-center">
        <!-- logo -->
        <svg
          class="w-24 h-24"
          fill="currentColor"
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
          version="1.1"
          viewBox="0 0 400 400"
          style="display: inline-block"
        >
          <defs>
            <clipPath id="uicons-juthajwuvp">
              <rect x="0" y="0" width="400" height="400" rx="0"></rect>
            </clipPath>
          </defs>
          <g clip-path="url(#uicons-juthajwuvp)">
            <g>
              <g>
                <path
                  d="M62.99998474121094,251.565L199.99998474121094,366L200.27298474121093,365.772L200.49998474121094,366L203.01798474121094,363.479L336.99998474121094,251.565L199.99998474121094,37L62.99998474121094,251.565ZM200.20898474121094,365.708L200.27298474121093,365.772L203.01798474121094,363.479L294.99998474121094,271.39099999999996L200.49998474121094,94L105.99998474121094,271.39099999999996L198.73798474121094,364.236L145.99998474121094,290.522L199.99998474121094,149L253.99998474121094,290.522L200.20898474121094,365.708Z"
                  fill-rule="evenodd"
                  fill="#56CB46"
                  fill-opacity="1"
                ></path>
              </g>
            </g>
          </g>
        </svg>
        <NH3>Nova - Admin</NH3>
        <transition name="fade-slide" mode="out-in">
          <component :is="formComponent[formType]" v-model="formType" class="w-[85%]" />
        </transition>
      </div>
    </NEl>
  </NEl>
</template>
{% endcodeblock %}
在 Naive UI 中`NEL`是一个通用的“元素容器”组件​​。NEl 本身没有默认样式（如边距、背景色等），只是一个干净的容器，方便你完全自定义。
在`NEL`中，可无缝使用 Naive UI 的 CSS 变量，比如上面代码中的`background-color: var(--body-color)`等都是Naive UI提供的主题变量。
虽然可以用普通 <div>，但 NEl 更符合 Naive UI 的设计体系

**下面是过渡动画样式：**
```css transition.css
/* fade-slide */
.fade-slide-leave-active,
.fade-slide-enter-active {
  transition: all 0.3s;
}
.fade-slide-enter-from {
  opacity: 0;
  transform: translateX(-30px);
}
.fade-slide-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
```

## naive-ui表单验证
> naive-ui表单验证：https://www.naiveui.com/zh-CN/os-theme/components/form

如果需要表单验证，naive-ui的`NForm`需要传递两个属性:
- `ref="formRef"`：比如`const formRef = ref<FormInst | null>(null)`
> FormInst 是 Naive UI 表单组件暴露的类型，包含表单的方法。
> 因为组件尚未挂载，所以初始化为null
- `:rules="rules"`: rules里面写校验规则：
比如：
```ts rules
const rules = {
  account: {
    required: true,
    trigger: 'blur',
    message: '请输入用户名',
  },
  password: {
    required: true,
    trigger: 'blur',
    message: '请输入密码',
  },
}
```

## 登录页
{% codeblock lang:ts 登录子组件 mark:22-25,47,60 %}
<script lang="ts" setup>
import {
  NButton,
  NCheckbox,
  NDivider,
  NFlex,
  NForm,
  NFormItem,
  NH2,
  NInput,
  NSpace,
  NText,
  type FormInst,
} from 'naive-ui'
import { Icon } from '@vicons/utils'
import WechatOutlined from '@vicons/antd/WechatOutlined'
import QqCircleFilled from '@vicons/antd/QqCircleFilled'
import GithubOutlined from '@vicons/antd/GithubOutlined'

import { ref, defineEmits } from 'vue'

const emits = defineEmits(['update:modelValue'])
const toOtherForm = (form: string) => {
  emits('update:modelValue', form)
}

const rules = {
  account: {
    required: true,
    trigger: 'blur',
    message: '请输入用户名',
  },
  password: {
    required: true,
    trigger: 'blur',
    message: '请输入密码',
  },
}

const formRef = ref<FormInst | null>(null)
const formValue = ref({
  account: 'super',
  pwd: '123456',
})
const isRemember = ref(false)

// 登录逻辑
const handleLogin = () => {
  formRef.value?.validate(() => {
    console.log('登录', formValue.value.account, formValue.value.pwd, isRemember.value)
  })
}
</script>

<template>
  <div>
    <NH2 class="text-center"> 登录 </NH2>

    <!-- 表单 -->
    <NForm ref="formRef" :rules="rules" :model="formValue" :show-label="false" size="large">
      <NFormItem path="account">
        <NInput v-model:value="formValue.account" clearable placeholder="请输入用户名" />
      </NFormItem>
      <NFormItem>
        <NInput
          v-model:value="formValue.pwd"
          type="password"
          show-password-on="click"
          placeholder="请输入密码"
        />
      </NFormItem>
      <NSpace vertical :size="20">
        <div class="flex items-center justify-between">
          <NCheckbox v-model:checked="isRemember"> 记住我 </NCheckbox>
          <NButton type="primary" text @click="toOtherForm('resetPwd')"> 忘记密码？ </NButton>
        </div>
        <NButton block type="primary" size="large" @click="handleLogin"> 登录 </NButton>
        <NFlex>
          <NText>没有账号？</NText>
          <NButton type="primary" text @click="toOtherForm('register')"> 注册 </NButton>
        </NFlex>
      </NSpace>
    </NForm>

    <NDivider><span class="opacity-70">或者</span></NDivider>

    <NSpace justify="center">
      <NButton circle>
        <template #icon>
          <Icon size="20">
            <WechatOutlined />
          </Icon>
        </template>
      </NButton>
      <NButton circle>
        <template #icon>
          <Icon size="20">
            <QqCircleFilled />
          </Icon>
        </template>
      </NButton>
      <NButton circle>
        <template #icon>
          <Icon size="20">
            <GithubOutlined />
          </Icon>
        </template>
      </NButton>
    </NSpace>
  </div>
</template>
{% endcodeblock %}

## 注册页
{% codeblock lang:ts 注册子组件 mark:16-19,48,67 %}
<script lang="ts" setup>
import {
  NButton,
  NCheckbox,
  NFlex,
  NForm,
  NFormItem,
  NH2,
  NInput,
  NSpace,
  NText,
  type FormInst,
} from 'naive-ui'
import { ref, defineEmits } from 'vue'

const emits = defineEmits(['update:modelValue'])
const toLogin = () => {
  emits('update:modelValue', 'login')
}

const rules = {
  account: {
    required: true,
    trigger: 'blur',
    message: '请输入用户名',
  },
  pwd: {
    required: true,
    trigger: 'blur',
    message: '请输入密码',
  },
  rePwd: {
    required: true,
    trigger: 'blur',
    message: '请输入确认密码',
  },
}

const formRef = ref<FormInst | null>(null)

const formValue = ref({
  account: 'admin',
  pwd: '000000',
  rePwd: '000000',
})
const isRead = ref(false)

// 注册逻辑
const handleRegister = () => {
  formRef.value?.validate(() => {
    console.log(
      '注册',
      formValue.value.account,
      formValue.value.pwd,
      formValue.value.rePwd,
      isRead.value
    )
  })
}
</script>

<template>
  <div>
    <NH2 class="text-center">注册</NH2>

    <!-- 表单 -->
    <NForm ref="formRef" :rules="rules" :model="formValue" :show-label="false" size="large">
      <NFormItem path="account">
        <NInput v-model:value="formValue.account" clearable placeholder="请输入用户名" />
      </NFormItem>
      <NFormItem path="pwd">
        <NInput
          v-model:value="formValue.pwd"
          type="password"
          show-password-on="click"
          placeholder="请输入密码"
        />
      </NFormItem>
      <NFormItem path="rePwd">
        <NInput
          v-model:value="formValue.rePwd"
          type="password"
          show-password-on="click"
          placeholder="请输入确认密码密码"
        />
      </NFormItem>
      <NFormItem>
        <NSpace vertical :size="20" class="w-full">
          <NCheckbox v-model:checked="isRead">
            <span>我已阅读并同意 </span>
            <NButton type="primary" text> 用户协议 </NButton>
          </NCheckbox>
          <NButton type="primary" block @click="handleRegister">注册</NButton>
          <NFlex justify="center">
            <NText>已有帐号？</NText>
            <NButton type="primary" text @click="toLogin">登录</NButton>
          </NFlex>
        </NSpace>
      </NFormItem>
    </NForm>
  </div>
</template>
{% endcodeblock %}

## 忘记密码页
{% codeblock lang:ts 忘记密码子组件 mark:15-18,33,45 %}
<script lang="ts" setup>
import {
  NButton,
  NFlex,
  NForm,
  NFormItem,
  NH2,
  NInput,
  NSpace,
  NText,
  type FormInst,
} from 'naive-ui'
import { ref, defineEmits } from 'vue'

const emits = defineEmits(['update:modelValue'])
const toLogin = () => {
  emits('update:modelValue', 'login')
}

const formRef = ref<FormInst | null>(null)
const rules = {
  account: {
    required: true,
    trigger: 'blur',
    message: '请输入账号或者手机号',
  },
}

const formValue = ref({
  account: '',
})

// 处理重置密码逻辑
const handleResetPwd = () => {
  formRef.value?.validate(() => {
    console.log('重置密码：', formValue.value.account)
  })
}
</script>

<template>
  <div>
    <NH2 class="text-center">重置密码</NH2>

    <NForm ref="formRef" :rules="rules" :show-label="false" size="large" :model="formValue">
      <NFormItem path="account">
        <NInput placeholder="输入账号\手机号" clearable />
      </NFormItem>
      <NFormItem>
        <NSpace vertical :size="20" class="w-full">
          <NButton block type="primary" @click="handleResetPwd"> 重置密码 </NButton>
          <NFlex justify="center">
            <NText>已有帐号？</NText>
            <NButton text type="primary" @click="toLogin">登录</NButton>
          </NFlex>
        </NSpace>
      </NFormItem>
    </NForm>
  </div>
</template>
{% endcodeblock %}

## 效果图
![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20250416211703965.png)
![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20250416211733602.png)
![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20250416211753206.png)