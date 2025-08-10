1. global 적용

```js
// main.js
import { createApp } from "vue";
import App from "./App.vue";
import "./assets/styles/global.css"; // 외부 CSS 파일 import

createApp(App).mount("#app");
```

2. 개별 컴포넌트 내에서 외부 CSS 파일 적용

```js
<template>
  <div class="example">외부 CSS 적용</div>
</template>

<style scoped src="./styles/example.css"></style>
```

```js
<template>
  <div class="box">
    <h1>안녕하세요</h1>
  </div>
</template>

<style scoped>
.box {
  border: 1px solid #ccc;
  padding: 10px;
}

h1 {
  color: red;
}
</style>
```
