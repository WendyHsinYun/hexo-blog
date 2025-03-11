---
title: 用 Vue Directive 管理角色權限
date: 2025-03-11 15:43:58
tags: 
  - directive
  - vue
---

### 前言
最近在專案遇到的需求是依照角色分配不同權限，並依照權限顯示相應功能。

role 的值是在 login 後，從後端回傳 response 取得並存在 localStorage，用 Store 來管理角色狀態。

原本我是在頁面上使用 computed 來及時從 store 獲得角色值，然後再用 `v-if` 控制是否顯示。但後來發現更好的寫法！於是做此紀錄。如果有朋友有更好的做法歡迎分享~


**備註: 以下程式碼都經過處理，沒有直接將專案程式碼複製貼上。只是要傳達做法，請依照各自專案再去配置。**

## 原本的方法: `v-if`

- 在 userStore 透過 localStorage 存取 Role 角色:

```javascript=
import { computed, ref } from "vue";
import { defineStore } from "pinia";

export const useUserStore = defineStore("user", () => {

  /** 使用者資訊 */
  const userInfo = ref({
    role: localStorage.getItem("userRole") || "",
  });

  return { isLoggedIn, userInfo };
});
```


- 在 utils 建立 hasRole 方法:
```javascript!=
import { storeToRefs } from 'pinia';
import { useUserStore } from '@/store/modules/user';

const userStore = useUserStore();
const { userInfo } = storeToRefs(userStore);

export const hasRole = (role: Role): boolean => {
  const userRole = userInfo.value.role;
  return role === userRole;
};
```

- 在 views 引入 hasRole 方法，判斷是否為某角色，template 區域用 v-if 來決定顯示該組件顯示與否。

```html=
<template>
 <MyButton v-if='!isPM'>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { hasRole } from '@/utils/role';

const isPM = computed(() => hasRole('PM'));
</script>
```

### 缺點
- 如果多出一個角色，就要再寫一個 `computed`。角色管理四散在不同的 views 檔案中。
- `v-if` 寫法較無判別性，難以即時排查。

----

## 使用 Directive 寫法

除了 Vue 原本提供的 `v-if`, `v-show` 等作法，我們也可以自己定義 `v-` 語法。

### 什麼情境適合
- 處理重複的工作，例如我在不同組件上要依照角色顯示功能
- 可全局註冊並套用在 DOM 上使用
- 可指定生命週期(例如 `mounted`) 

### 最終目標

只要在 views 的 components 加上 `v-hide-for="['PM', 'RD']"`，只要用這兩種角色登入，就無法看到這個組件。全局通用，且不需要額外在  `<script setup>`定義。


```html=
<PrimaryButton
  v-hide-for="['PM', 'RD']"`
/>
```

### 優點
- 邏輯都放在 directives 集中處理，比較好維護跟擴充
- 不用在每個 views 都用 `computed` 定義，而是全局通用
- 看起來直覺多了! 

### 官方文件 [ref](https://zh-hk.vuejs.org/guide/reusability/custom-directives#directive-hooks)

```javascript=
const myDirective = {
  // 在綁定元素的父組件
  // 及他自己的所有子節點都掛載完成後調用
  mounted(el, binding, vnode, prevVnode) {},
}
```

**參數(都是可選的)**
- el：指令綁定到的元素。這可以用於直接操作 DOM。
- binding：一個對象，包含各種屬性，我使用的就是 value：傳遞給指令的值。

### 實際作法

1. 在 src 資料夾創造 `directives` 資料夾，創造 hideFor.ts 文件

```javascript=
import type { Directive } from 'vue';
import { storeToRefs } from 'pinia';
import { useUserStore } from '@/store/modules/user';

const hideForDirective: Directive = {
  mounted(el, binding) {
    const userStore = useUserStore();
    const { userInfo } = storeToRefs(userStore);
    const excludedRoles = binding.value;

    if (excludedRoles.includes(userInfo.value.role)) {
      el.parentNode?.removeChild(el);
    }
  }
};

export default hideForDirective;

```


2. 在 main.ts 做全局註冊
```javascript=
import hideForDirective from '@/directives/hideFor';
import App from './App.vue';

async function setupApp() {
  const app = createApp(App);

  setupStore(app);
    
  app.directive('hideFor', hideForDirective);

  app.mount('#app');
}

setupApp();
```

3. 隱藏你想隱藏的吧!

在 views 的組件上加 `v-hide-for="['PM']"`，然後當我用 'PM' 的角色登入後，我就看不到這個 Button 嚕。

```html=
<PrimaryButton
  v-hide-for="['PM']"`
/>