# Vue 컴포넌트 생명주기 흐름

1. 생성 단계 (Creation)

- 컴포넌트가 메모리에 만들어지는 단계

- 아직 DOM에 붙지 않음 (화면에 보이지 않음)

- API 호출, 초기 데이터 세팅 가능 (DOM 조작은 불가)

2. 마운트 단계 (Mounting)

- 컴포넌트가 실제 DOM에 연결되어 화면에 표시됨

- 여기서부터 DOM 조작 가능

3. 업데이트 단계 (Updating)

- 반응형 데이터가 바뀌어 화면이 다시 렌더링되는 단계

4. 언마운트 단계 (Unmounting)

- 컴포넌트가 화면에서 제거되는 단계

- 이벤트 리스너, 타이머 해제 필요

# 2. Vue 3 주요 Lifecycle Hooks

| 훅 이름           | 실행 시점                            |
| ----------------- | ------------------------------------ |
| `onBeforeMount`   | DOM에 붙기 직전                      |
| `onMounted`       | DOM에 붙은 직후 (DOM 조작 가능)      |
| `onBeforeUpdate`  | 반응형 데이터가 바뀌어 DOM 갱신 직전 |
| `onUpdated`       | DOM이 갱신된 직후                    |
| `onBeforeUnmount` | 컴포넌트가 제거되기 직전             |
| `onUnmounted`     | 컴포넌트가 제거된 직후               |

```js
<script setup>
import { ref, onBeforeMount, onMounted, onBeforeUpdate, onUpdated, onBeforeUnmount, onUnmounted } from 'vue'

const count = ref(0)

onBeforeMount(() => {
  console.log('📌 DOM에 붙기 직전')
})

onMounted(() => {
  console.log('✅ DOM에 붙은 후')
})

onBeforeUpdate(() => {
  console.log('📌 DOM 업데이트 직전')
})

onUpdated(() => {
  console.log('🔄 DOM 업데이트 직후')
})

onBeforeUnmount(() => {
  console.log('📌 컴포넌트 제거 직전')
})

onUnmounted(() => {
  console.log('🗑 컴포넌트 제거 후')
})

function add() {
  count.value++
}
</script>

<template>
  <div>
    <p>{{ count }}</p>
    <button @click="add">+1</button>
  </div>
</template>

```

# 사용 시 주의점

- API 호출 → onMounted에서 하는 것이 일반적 (DOM 접근 가능)
- 타이머, 이벤트 등록 → onMounted에서 등록하고 onUnmounted에서 해제
- 데이터 초기화는 setup() 또는 onBeforeMount에서 가능

# setup

```js
<script setup>
import { ref } from 'vue'

const count = ref(0)

function increment() {
  count.value++
}
</script>

<template>
  <button @click="increment">Count: {{ count }}</button>
</template>
```

- 위는 `<script setup>` 문법을 사용한 예시로, 별도의 setup() 함수를 직접 쓰지 않아도 내부적으로 setup()에서 실행

```js
<script>
import { ref } from 'vue'

export default {
  setup(props, context) {
    const count = ref(0)

    function increment() {
      count.value++
    }

    return { count, increment }
  }
}
</script>

<template>
  <button @click="increment">Count: {{ count }}</button>
</template>

```

- 위는 일반 setup() 함수 선언 방식
- props, context(emit, attrs 등)를 인자로 받음
- 반환값이 템플릿에 바인딩됨
