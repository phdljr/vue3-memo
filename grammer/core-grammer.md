# 1. ref()

- 단일 값(문자, 숫자, 불린 등)을 반응형으로 만드는 함수
- .value를 통해 접근/변경

```js
<script setup>
import { ref } from 'vue'

const count = ref(0)

function increment() {
  count.value++
}
</script>

<template>
  <p>{{ count }}</p>
  <button @click="increment">+1</button>
</template>
```

# 2. reactive()

- 객체나 배열을 반응형으로 만드는 함수
- ref()와 달리 .value 없이 바로 접근 가능
- 반응형 객체 전체를 재할당하면 반응성이 깨질 수 있음

```js
<script setup>
import { reactive } from 'vue'

const user = reactive({
  name: '홍길동',
  age: 25
})

function growOlder() {
  user.age++
}
</script>

<template>
  <p>{{ user.name }} ({{ user.age }})</p>
  <button @click="growOlder">나이 +1</button>
</template>

```

# 3. computed()

- 기존 데이터(state)를 기반으로 계산된 값을 만드는 함수
- 자동으로 종속성을 추적하고, 종속 데이터가 바뀌면 값이 갱신

```js
<script setup>
import { ref, computed } from 'vue'

const price = ref(1000)
const tax = ref(0.1)

const totalPrice = computed(() => price.value * (1 + tax.value))
</script>

<template>
  <p>총 가격: {{ totalPrice }}</p>
</template>
```

# 4. watch()

- 특정 반응형 데이터의 변화를 감지해 부가 동작을 수행

```js
<script setup>
import { ref, watch } from 'vue'

const name = ref('')

watch(name, (newVal, oldVal) => {
  console.log(`이름 변경: ${oldVal} → ${newVal}`)
})
</script>

<template>
  <input v-model="name" placeholder="이름 입력" />
</template>
```

# 5. props

- 부모 → 자식 컴포넌트 데이터 전달
- Vue 3에서는 `<script setup>에서 defineProps()`를 사용

```js
<!-- Parent.vue -->
<template>
  <Child title="안녕하세요" />
</template>

<!-- Child.vue -->
<script setup>
const props = defineProps({
  title: String
})
</script>

<template>
  <h1>{{ props.title }}</h1>
</template>

```

# 6. emit

- 자식 → 부모 컴포넌트 이벤트 전달
- defineEmits()를 사용

```js
<!-- Parent.vue -->
<template>
  <Child @send="receiveMessage" />
</template>

<script setup>
function receiveMessage(msg) {
  alert(`자식으로부터: ${msg}`)
}
</script>

<!-- Child.vue -->
<script setup>
const emit = defineEmits(['send'])

function sendMessage() {
  emit('send', '안녕하세요 부모님!')
}
</script>

<template>
  <button @click="sendMessage">보내기</button>
</template>
```

# 7. v-if / v-else-if / v-else

- 조건부 렌더링

```js
<template>
  <p v-if="age >= 20">성인입니다</p>
  <p v-else-if="age >= 13">청소년입니다</p>
  <p v-else>어린이입니다</p>
</template>
```

# 8. v-for

- 반복 렌더링

```js
<template>
  <ul>
    <li v-for="(item, index) in items" :key="index">{{ item }}</li>
  </ul>
</template>

<script setup>
const items = ['사과', '바나나', '포도']
</script>
```

# 9. v-model

- 양방향 데이터 바인딩

```js
<script setup>
import { ref } from 'vue'

const text = ref('')
</script>

<template>
  <input v-model="text" placeholder="입력하세요" />
  <p>입력값: {{ text }}</p>
</template>
```

# 10. v-bind (:) & @

- v-bind (속성 바인딩): `<img :src="imgUrl" />`
- @ (이벤트 바인딩): `<button @click="clickEvent">클릭</button>`

# 11. slot

- 부모에서 자식 컴포넌트로 HTML 구조 전달

```js
<!-- Parent.vue -->
<Child>
  <p>이 내용은 자식에 슬롯으로 들어갑니다.</p>
</Child>

<!-- Child.vue -->
<template>
  <div class="box">
    <slot></slot>
  </div>
</template>
```

# 12. Lifecycle Hooks

- 컴포넌트의 생성~소멸 시점에 동작하는 함수

```js
<script setup>
  import {(onMounted, onUnmounted)} from 'vue' onMounted(() =>{" "}
  {console.log("컴포넌트가 마운트됨")}) onUnmounted(() =>{" "}
  {console.log("컴포넌트가 해제됨")})
</script>
```
