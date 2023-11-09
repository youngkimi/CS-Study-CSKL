# TOPIC 1

## QUESTIONS

### 1️⃣.

### 2️⃣.

### 3️⃣.

### 4️⃣.

### 5️⃣.

### 6️⃣.

### 7️⃣.

### 8️⃣.

### 9️⃣.

### 🔟.

# TOPIC 2

## QUESTIONS

### 1️⃣.

### 2️⃣.

### 3️⃣.

### 4️⃣.

### 5️⃣.

### 6️⃣.

### 7️⃣.

### 8️⃣.

### 9️⃣.

### 🔟.

# TOPIC 3

## QUESTIONS

### 1️⃣.

### 2️⃣.

### 3️⃣.

### 4️⃣.

### 5️⃣.

### 6️⃣.

### 7️⃣.

### 8️⃣.

### 9️⃣.

### 🔟.

# TOPIC 4 SFC

## QUESTIONS

### 1️⃣. App과 MyComponent의 텍스트 색깔을 무엇인가?.
<!-- App.vue-->
```vue
<template>
  <div>
    <h2>App</h2>
    <MyComponent/>
  </div>
</template>

<script setup>
import MyComponent from './components/MyComponent.vue';
</script>

<style>
</style>
```

<!-- MyComponent.vue-->
```vue
<template>
    <div>
        <h3>MyComponent</h3>
    </div>
</template>

<script setup>
</script>

<style>
div {
  color: red;
}
</style>
```

### 2️⃣. Virtual DOM의 장점에 대해 작성하시오.

### 3️⃣. SFC의 특징에 대해 작성하시오.

### 4️⃣. script setup을 통해 컴포넌트의 각 인스턴스를 실행하는 경우 기존 .html에서 script를 사용하는 것에 비해 어떤 효과가 있는가?

### 5️⃣. Vue 앱이 SPA(Single Page Application)인 이유가 무엇인가?

### 6️⃣. 절대 경로를 사용하기 위한 특수문자는 무엇인가?

### 7️⃣. 규모가 있는 프로젝트의 경우 Open API를 자주 사용하기에 Option API를 권장한다. (O / X)

### 8️⃣. style 시트의 scoped의 기능에 대해 설명하시오.

### 9️⃣. Vite 프로젝트의 구조 중 정확한 버전, 일관성 있는 의존성을 유지하기 위한 파일은 무엇인가?

### 🔟. vue를 실행하면서 index.html로 실행될 때 렌더링 되지 않고 사라지는 태그는 무엇인가?

# TOPIC 5 STATE

## QUESTIONS

### 1️⃣. props의 바인딩 방식은?
        1. 상향식 단방향 바인딩
        2. 상향식 양방향 바인딩
        3. 하향식 단방향 바인딩
        4. 하향식 양방향 바인딩

### 2️⃣. props의 특징으로 틀린 것은?
        1. 자식 컴포넌트 내부에서 props를 변경하려고 시도해서는 안되며 불가능하다.
        2. 부모 컴포넌트가 자식 컴포넌트에 데이터를 전달하는데 사용되는 속성이다.
        3. 모든 props는 단방향 바인딩을 형성한다.
        4. 부모 컴포넌트에서 업데이트 후 서버를 재실행시켜야 자식 컴포넌트의 모든 props가 업데이트된다.
        5. props를 script 태그 내에서 접근할 수 있다.

### 3️⃣. 각각 props의 타입을 써라.
```html
A : <SomeComponent num-props="1" />
B : <SomeComponent :num-props="1" />
```

### 4️⃣. props 및 emit 이벤트 선언 시 객체 선언 문법을 권장하는 이유는?

### 5️⃣. 자식 컴포넌트에서 이벤트 보낼 때 빈칸 채우기
```html
<!-- 자식 -->
<button @click="__________________">클릭</button>
```
```html
<!-- 부모 -->
<Parent @some-event="someCallback" />
```

### 6️⃣. Component 간 event 전달 시 틀린 것
        1. 템플릿 표현식에서 직접 사용자 정의 이벤트를 발신할 수 있다.
        2. 부모는 v-on을 사용하여 수신한다.
        3. emit 이벤트를 객체 선언 문법으로 작성할 수 있다.
        4. 이벤트 발신 시 추가 인자를 전달하여 값을 제공할 수 없다.

### 7️⃣. emit 이벤트 선언 시 빈칸 채우기
```jsx
<!-- 자식 -->
<script setup>
const emit = ___________(['someEvent'])
const buttonClick = function () {
    emit('someEvent')
}
</script>
```

# TOPIC 6

## QUESTIONS

### 1️⃣.

### 2️⃣.

### 3️⃣.

### 4️⃣.

### 5️⃣.

### 6️⃣.

### 7️⃣.

### 8️⃣.

### 9️⃣.

### 🔟.

# TOPIC 7

## QUESTIONS

### 1️⃣.

### 2️⃣.

### 3️⃣.

### 4️⃣.

### 5️⃣.

### 6️⃣.

### 7️⃣.

### 8️⃣.

### 9️⃣.

### 🔟.

