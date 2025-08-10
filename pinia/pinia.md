- Vue 3에서 Pinia는 공식 상태 관리 라이브러리
- Vuex보다 문법이 간단하고 TypeScript 친화적

```
npm install pinia
```

```js
import { createApp } from "vue";
import App from "./App.vue";
import { createPinia } from "pinia";

const app = createApp(App);
app.use(createPinia());
app.mount("#app");
```

```js
import { defineStore } from "pinia";
import { ref } from "vue";

export const useUserStore = defineStore("user", () => {
  const name = ref("");
  const isLogin = ref(false);

  function login(username) {
    name.value = username;
    isLogin.value = true;
  }

  function logout() {
    name.value = "";
    isLogin.value = false;
  }

  return { name, isLogin, login, logout };
});
```

```js
<script setup>
import { useUserStore } from '@/stores/user'

const userStore = useUserStore()

function doLogin() {
  userStore.login('홍길동')
}
</script>

<template>
  <div>
    <p v-if="userStore.isLogin">
      {{ userStore.name }}님 로그인됨
    </p>
    <button @click="doLogin">로그인</button>
    <button @click="userStore.logout">로그아웃</button>
  </div>
</template>
```

### Pinia 장점

- 간단한 API → state, getter, action 구분이 명확
- TypeScript 친화 → 자동 타입 추론
- Vue Devtools 지원 → 상태 디버깅 편리
- Composition API와 잘 어울림
