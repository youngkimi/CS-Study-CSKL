### 🔍# 💡 TOPIC 1 INTRO

#### 김병현

### 🔍

### 🔍

### 🔍

### 🔍

# 💡 TOPIC 2 Syntax1

#### 김예림, 김병현

### 🔍

## Dynamically data binding(v-bind)

<aside>
💡 하나 이상의 속성 또는 컴포넌트 데이터를 표현식에 동적으로 바인딩

</aside>

### Attribute Bindings

```html
<img :src="imageSrc" />
<a :href="myUrl">Move to Url</a>
<p :[dynamicattr]="dynamicValue">동적 바인딩</p>
**<!-- 여기서 :는 v-bind의 약어 -->**
```

✨ 대괄호 안에 작성하는 이름은 반드시 소문자로만 구성 가능

(브라우저가 속성 이름을 소문자로 강제 변환)

### Class and Style Bindings

1. Binding HTML Classes

   - 객체를 :class에 전달하여 클래스를 동적으로 전환할 수 있음

   ```jsx
   const isActive = ref(false);
   // isActive 값에 따라 아래 class에 active의 추가 여부가 결정됨
   ```

   ```html
   <div :class="{active: isActive}">Text</div>
   ```

   - 여러 클래스 전환

   ```jsx
   const isActive = ref(false);
   const hasInfo = ref(true);
   ```

   ```html
   <div class="static" :class="{active: isActive, 'text-primary': hasInfo }">
     Text
   </div>
   ```

   - 객체 방식

   ```jsx
   const isActive = ref(false);
   const hasInfo = ref(true);

   const classObj = ref({
     active: isActive,
     'text-primary': hasInfo,
   });
   ```

   ```html
   <div class="static" :class="classObj">Text</div>
   ```

   - 배열 바인딩

   ```jsx
   const activeClass = ref('active');
   const infoClass = ref('text-primary');
   ```

   ```html
   <div :class="[activeClass, infoClass]">Text</div>
   ```

   - 배열 + 객체

   ```html
   <div :class="[{active: isActive}, infoClass]">Text</div>
   ```

2. Binding Inline Styles

   - inline-style 바인딩 (단, kebab-cased 문자열도 지원 → camelCase 권장)

   ```jsx
   const activeClass = ref('crimson');
   const fontSize = ref(50);
   ```

   ```html
   <div :style="{color: activeColor, fontSize: fontSize + 'px'}">Text</div>
   <div :style="{'font-size': fontSize + 'px'}">Text</div>
   ```

   - Objects에 바인딩, 배열 바인딩 가능

   ```jsx
   const styleObj = ref({
     color: activeColor,
     fontSize: fontSize.value + 'px',
   });
   ```

   ```html
   <div :style="styleObj">Text</div>
   <div :style="[styleObj, styleObj2]">Text</div>
   <!-- 결과 -->
   <div style="color: blue; font-size: 50px; border: 1px solid black;">
     Text
   </div>
   ```

## Event Handling (v-on)

<aside>
💡 DOM 요소에 이벤트 리스너를 연결 및 수신

</aside>

```jsx
v-on:event="handler"
=> @event="handler" // 약어
```

### Handler 종류

1. Inline handlers: 이벤트가 트리거 될 때 실행 될 JS 코드

   주로 간단한 상황에 사용

   ```html
   <button @click="count++">Add 1</button>
   <p>Count: {{ count }}</p>
   ```

2. Method handlers: 컴포넌트에 정의될 메서드 이름

   ✔️ 1번이 불가능한 대부분의 상황에서 사용

   ✔️ Method Handlers를 트리거 하는 기본 DOM Event 객체를 자동을 수신

   ```jsx
   const myFunc = (event) => {
     console.log(event);
     console.log(event.currentTarget);
     console.log(event.target.innerText);
   };
   ```

   ```html
   <p @click="myFunc">테스트</p>
   ```

   ![Untitled](../VUE/assets/test.png)

   ✔️ 인자를 전달하여 메서드 호출도 가능

   ```jsx
   const myFunc = (message) => {
     console.log(message);
   };
   ```

   ```html
   <p @click="myFunc('test')">테스트</p>
   ```

   ✔️ 인자와 이벤트 객체 모두 사용하고 싶다면 ? **($event 사용)**

   ```jsx
   const myFunc = (message, event) => {
     console.log(message);
     console.log(message);
   };
   ```

   ```html
   <p @click="myFunc('test', $event)">테스트</p>
   ```

### Event Modifiers

.stop, .prevent, .self, .capture, .once, .passive

```jsx
<!-- 클릭 이벤트 전파가 중지됩니다. -->
<a @click.stop="doThis"></a>

<!-- submit 이벤트가 더 이상 페이지 리로드하지 않습니다. -->
<form @submit.prevent="onSubmit"></form>

<!-- 수식어를 연결할 수 있습니다. -->
<a @click.stop.prevent="doThat"></a>

<!-- 이벤트에 핸들러 없이 수식어만 사용할 수 있습니다. -->
<form @submit.prevent></form>

<!-- event.target이 엘리먼트 자신일 경우에만 핸들러가 실행됩니다. -->
<!-- 예를 들어 자식 엘리먼트에서 클릭 액션이 있으면 핸들러가 실행되지 않습니다. -->
<div @click.self="doThat">...</div>

<!-- 이벤트 리스너를 추가할 때 캡처 모드 사용 -->
<!-- 내부 엘리먼트에서 클릭 이벤트 핸들러가 실행되기 전에, 여기에서 먼저 핸들러가 실행됩니다. -->
<div @click.capture="doThis">...</div>

<!-- 클릭 이벤트는 단 한 번만 실행됩니다. -->
<a @click.once="doThis"></a>

<!-- 핸들러 내 `event.preventDefault()`가 포함되었더라도 -->
<!-- 스크롤 이벤트의 기본 동작(스크롤)이 발생합니다.        -->
<!-- 모바일 장치의 성능 향상을 위해 터치 이벤트 리스너와 함께 사용 -->
<div @scroll.passive="onScroll">...</div>
```

```html
<form @submit.prevent="onSubmit"></form>
```

**❌ 유의할 점**

1. vue에서 v-on에 대한 Event Modifiers를 제공하기 때문에 event.preventDefault()와 같은 구문을 메서드에서 작성하지 말 것
2. Modifiers는 chained 되게끔 작성할 수 있으며 작성된 순서로 실행되기 때문에 작성 순서에 유의할 것

### Key Modifiers

키보드 이벤트를 수신할 때 특정 키에 관한 별도 modifiers를 사용가능

```html
<input @keyup.enter="onSubmit" />
```

## Form Input Bindings

form을 처리할 때 사용자가 input에 입력하는 값을 실시간으로 JavaScript 상태에 동기화 해야하는 경우 ⇒ **양방향 바인딩**

### 1. v-bind와 v-on을 함께 사용

@input과 :value를 함께 사용

v-bind를 사용하여 input요소의 value 속성 값을 입력값으로 사용,

v-on을 사용하여 input 이벤트가 발생할 때마다 input의 value 값을 별도 반응형 변수에 저장하는 핸들러 onInput을 호출

```jsx
const inputText1 = ref('');
const **onInput** = (event) = {
	inputText1.value = event.currentTarget.value;
};
```

```html
<p>{{ inputText1 }}</p>
<input **:value="inputText1" @input="onInput" ** />
```

✨ IME(입력기)가 필요한 언어(한국어, 중국어, 일본어)의 경우 v-model이 제대로 업데이트 되지 않아서 v-bind와 v-on을 사용해야 함

### 2. v-model 사용

v-model을 사용하여 사용자 입력 데이터와 반응형 변수를 실시간 동기화

```jsx
const **inputText2** = ref('');
```

```html
<p>{{ inputText2 }}</p>
<input **v-model="inputText2" ** />
```

✔️ checkbox 활용했을 때

1. 단일

```html
<input type="checkbox" id="checkbox" **v-model="checked" ** />
<label for="checkbox">{{ checked }}</label>
```

1. 여러개 활용

```jsx
const checkedNames = ref([]);
```

```html
<input type="checkbox" id="alice" value="Alice" **v-model="checkedNames" ** />
<label for="alice">Alice</label>
<input type="checkbox" id="bella" value="Bella" **v-model="checkedNames" ** />
<label for="bella">Bella</label>
```

✔️ select 활용했을 때

초기 값이 어떤 option과도 일치하지 않을 때, “선택되지 않은(unselected)”상태로 렌더링

```jsx
const selected = ref('');
```

```html
<div>Selected: {{ selected }}</div>

<select v-model="selected">
  <option disabled value="">Please select one</option>
  <option>Alice</option>
  <option>Bella</option>
  <option>Cathy</option>
</select>
```

# 💡 TOPIC 3 Syntax2

#### 석지명

### 🔍

### 🔍

### 🔍

### 🔍

# 💡 TOPIC 4 SFC

#### 김종인

## Single-File Components
- Component
  - COmponent란 하나의 덩어리로서, 재사용 가능한 코드 블록을 의미한다.
  - UI를 독립적이고 재사용 가능한 일부분으로 분할하고 각 부분을 개별적으로 다룰 수 있음. 이에 따라 앱은 자연스럽게 중첩된 Component의 트리로 구성된다.
- Single-FIle Component (SFC)
  - 컴포넌트의 템플릿, 로직 및 스타일을 하나의 파일로 묶어낸 특수한 파일 형식 (*.vue 파일)
  - HTML, CSS 및 JavaScript 3개를 하나로 합친 것
  - template에서 HTML을, scrpit에서 JS와 Vue 인스턴스를 style에서 CSS를 하나의 파일에서 컴포넌트의 뷰, 로직 및 스타일을 캡슐화하고 배치

### 🔍 Single-File Components 문법
- 최상위 언어 블록
  - template, script, style이며 일반적으로 해당 순서로 작성
  -  *.vue 파일은 template, script setup의 경우 단 1개의 태그만 포함할 수 있지만 style의 경우 여러 태그가 포함될 수 있다.
- template
  - 예를 들어, template 안에 div 태그가 2개 오는 경우가 있는데 현재 vue3 버전에서는 오류가 발생하지는 않지만 권장하지 않음. (vue2는 오류 발생)
  - template 태그는 렌더링 되지 않고 사라진다.
- script setup
  - 컴포넌트의 setup() 함수로 사용되며 컴포넌트의 각 인스턴스에 대해 실행함
    - setup()을 통해서 return을 해주는 경우에서는 모든 코드에 대해 return을 작성하는 불편함이 있었다.
- style scoped
  - scoped가 지정되면 CSS는 현재 컴포넌트에만 적용 (scoped가 없다면 다른 컴포넌트에도 적용되므로 주의!)

## SFC build tool (Vite)
- 프론트엔드 개발 툴 (Vue에만 한정하지 않음)
- node.js를 설치해서 npm을 사용할 수 있음.
- 우리가 이후에 router를 배우면서 SPA(Single Page Application) -> 여러 페이지로 갈 수 있음.

### 🔍 Node.js
- 정의: Chrome의 V8 JavaScrpit 엔진을 기반으로 하는 Server-Side 실행환경
- 영향
  - 기존에 브라우저 안에서만 동작할 수 있었던 JavaScript를 브라우저가 아닌 서버 측에서도 실행할 수 있게 함
    - 프론트 엔드와 백엔드에서 동일한 언어로 개발 할 수 있게 됨
  - NPM(Node Package Manager)을 활용해 수많은 오픈 소스 패키지와 라이브러리를 제공하여 개발자들이 손쉽게 코드를 공유하고 재사용할 수 있게 함

### 🔍 Vite 프로젝트 구조
- node_modules
  - 외부 패키지들이 저장되는 디렉토리
  - 프로젝트의 의존성 모듈을 저장하고 관리하는 공간
  - node_modules 파일은 .gitignore에 작성되기 때문에 공유가 되지 않는다.
- package-lock.json
  - node_modules에 들어있거나 해당 프로제트의 정보를 저장하는 파일
    - 예를 들어, 이전에 A라는 사람이 axios 1버전을 사용하여 작업했으나 이후에 B라는 사람이 axios 3버전을 이용해서 작업하면 버전이 달라 의존 관계 등 동작이 제대로 되지 않을 수 있는 현상을 방지한다.
    - 정확한 버전 보장, 일관성 있는 의존성 유지로 패키지 설치에 필요한 모든 정보를 포함
- public 디렉토리
  - 정적 파일 위치 (참조되지 않는 소스 코드, 같은 이름을 갖고 import할 필요 없는 파일)
  - 항상 root 절대 경로를 사용하여 참조
- src 디렉토리
  - 주요 소스 코드를 포함하는 곳
  - 컴포넌트, 스타일, 라우팅 등 프로젝트의 핵심 코드 관리
  - assets
    - 이미지, 폰트, 스타일 시트 등을 관리하며 컴포넌트 자체에서 참조하는 내부 파일을 저장하는데 사용 (우리가 삭제하는 base.css, logo.svg, main.css 등)
  - components
    - Vue 컴포넌트를 작성하는 곳 (SFC 파일들을 저장하는 폴더), App.vue는 components 폴더 내에 포함되어 있지 않음.
  - App.vue
    - Vue 앱의 최상위 Root 컴포넌트로 다른 하위 컴포넌트들을 포함하며 어플리케이션 전체의 레이아웃과 공통적인 요소를 정의
  - main.js
    - Vue 인스턴스를 생성하고, 어플리케이션을 초기화 하는 역할로서 필요한 라이브러리를 import하고 전역 설정을 수행하는 역할을 한다.
  - index.html
    - Root 컴포넌트인 App.vue가 해당 페이지에 마운트 되기 때문에 Vue 앱이 SPA인 이유이다. (index.html 파일이 1개밖에 없어서)
    - Vue 앱의 기본 HTML 파일, 앱의 진입점, 필요한 스타일 시트 및 스크립트 등의 외부 리소스를 로드할 수 있음.

## Virtual DOM

### 🔍 Virtual DOM의 정의
- 웹 성능 향상을 위한 Vue의 렌더링 기술로 실제 DOM과 변경 사항 비교를 통해 변경된 부분만 실제 DOM에 적용하는 방식
- 실제 DOM을 조작하는 것은 느리지만 가상 DOM을 조작하는 것은 빠르다.
![DOM](./assets/DOM.png)

### 🔍 Virtual DOM의 장점
- 효율성
  - 실제 DOM 조작을 최소화 하고, 변경된 부분만 업데이트 (성능 향상)
- 반응성
  - 데이터의 변경을 감지(Watch, Computed), Virtual DOM을 효율적으로 갱신하여 UI를 자동으로 업데이트
    - Computed : 나와 직접적으로 관련되어 있는 것이 값이 변화가 생긴다면 바뀐 값으로 변화를 시켜주고 캐싱을 하고있다. (데이터가 바뀌지 않으면 이미 내가 저장한 값이 있으니 다시 계산을 하지 않음)
    - watch : 나와 직접적으로 관련되어 있거나 아닌 것들을 감시하
- 추상화
  - 조작은 Vue가 개발자는 실제 DOM 조작만 진행

### 🔍 Virtual DOM 주의사항
- 실제 DOM에 직접 접근하지 말 것 (직접 접근이 필요한 경우는 ref를 통해서 할 것)
  - querySelector 대신 bind 또는 변수를 선언하거나 addEventListener 대신 v-on(@)을 통해 이벤트 감지한다.

### 🔍 Virtual DOM 주의사항
- Composition API (규모가 있는 프로젝트) -> 권장
  - script setup 안에 한 곳에 변수나 메서드를 한 곳에서 모아서 사용
- Option API (복잡성이 낮은 프로젝트)
  - data 안에 변수 선언, methods 안에 메서드 선언, mounted를 통해 컴포넌트를 정의함
  - Option API의 경우에는 변수와 메서드가 분리되서 선언되기 때문에 코드가 길 경우에 해당 메서드의 변수가 어떤 것인지 확인하는데 어려움이 있다.

## 참고
- Scaffolding (스캐폴딩) : 초기구조와 기본 코드를 자동으로 생성
- scoped 기능 : 부모컴포넌트의 스타일이 자식 컴포넌트로 유출되지 않음
  - scoped 예시
```Vue
<!-- App.vue-->
<template>
  <h1>App.vue</h1>
  <MyComponent />
</template>

<style scoped>
div {
  color: red'
}
</style>
```

```Vue
<!-- MyComponent.vue-->
<template>
  <div>
    <h2>MyComponent</h2>
  </div>
</template>
```
위의 경우, MyComponent는 App.vue의 자식으로서 부모와 본인의 CSS 모두 영향을 받기 때문에 글자색이 red이다.

# 💡 TOPIC 5 STATE

#### 이승헌

### 🔍

### 🔍

### 🔍

### 🔍

# 💡 TOPIC 6 라우터

#### 조현수

### 🔍 Routing

네트워크에서 경로를 선택하는 프로세스. 웹 어플리케이션에서 다른 페이지 간의 전환과 경로를 관리하는 기술

1. **SSR (Server Side Rendering)**
   - 서버에서 사용자에게 보여줄 페이지를 모두 구성하여 사용자에게 페이지를 보여주는 방식 (JSP, Servlet)
2. **CSR (Client Side Rendering)**
   - 처음 로드될때 전체 페이지를 다 받아온 후에, 클라이언트 측에서 필요한 컴포넌트를 랜더링 하는 방식. 즉 페이지는 한 개이지만 링크에 따라 여러 컴포넌트를 랜더링 하여 마치 여러 페이지를 사용하는 것처럼 구성한다.
3. **SPA ( Single Page Application)**
   - 서버로부터 새로운 페이지를 불러오지 않고 페이지를 동적으로 불러와서 사용하는 웹어플리케이션

### 🔍 RouterLink

- 페이지를 로드하지 않고 URL을 변경하는 로직 처리
- HTML의 a태그를 렌더링

```html
<template>
    <nav>
        <RouterLink to="/" > Home <RouterLink>
        <RouterLink to="/about" > About <RouterLink>
    </nav>
</template>

```

### 🔍 RouterView

- URL에 해당하는 컴포넌트를 표시
- 원하는 레이아웃에 배치
- views폴더에 RouterView 위치에 렌더링 할 컴포넌트를 배치
- 일반 컴포넌트와 구분하기 위해 이름을 View로 끝나도록 작성

```html
<template>
    <nav>
        <RouterLink to="/" > Home <RouterLink>
        <RouterLink to="/about" > About <RouterLink>
        <RouterLink :to="{name: 'home'}" > Home <RouterLink>
        <RouterLink :to="{name: 'about'}" > About <RouterLink>
        <RouterLink :to="{name: 'user', params:{id: 'ssafy'}}"김싸피</RouterLink>
    </nav>

    <!-- 페이지를 렌더링 하고 싶은 곳에 배치-->
    <RouterView/>
</template>

<script setup>
    import { RouterView, RouterLink } from 'vue-router';

</script>
```

### 🔍 Router 활용

### index.js

```js
import HomeView from '../views/HomeView.vue';
import AboutView from '@/views/AboutView.vue';
import UserView from '@/views/UserView.vue';

const router = createRouter({
  routes: [
    //HomeView
    {
      path: '/',
      name: 'home',
      component: HomeView,
    },
    //AboutView
    {
      path: '/about',
      name: 'about',
      component: AboutView,
    },
    //UserView - 동적 경로 매칭
    {
      path: '/user/:id', //매개변수 표시
      name: 'user',
      component: UserView,
    },
  ],
});
```

### UserView.vue

```html
<template>
    <div>
        <h1>UserView<h1>
        <!--첫번째 방법 : $route.params로 참조-->
        <!-- 추천 하지 않음 -->
        {{$route.params.id}}

        <!--두번째 방법-->
        <!-- 이와 같이 작성 권장-->
        <!-- Composition API 방식-->
        {{userId}}
    </div>
</template>

<script setup>
    import {ref} from 'vue'

    //router를 적용하기 위한 설정
    import {useRoute} from 'vue-router'

    const route = useRoute()

    //route.params.id의 값을 ref변수 userId에 담아서 template 영역과 동적 경로 매칭
    const userId = ref(route.params.id)
</script>

```

### 🔍 프로그래밍 방식 네비게이션

1. router.push() -> 다른 위치로 이동
2. router.replace() -> 현재 위치 바꾸기

### router.push()

- 다른 URL로 이동
- **새 항목을 history stack에 push하는 방식 -> 브라우저 뒤로가기 버튼 클릭시 이전 URL로 이동 가넝**
- RouterLink 클릭할 때 내부적으로 호출되는 메서드이므로 동일한 방식

선언적 : `<RouterLink :to=""/>`

프로그래밍적 : `router.push(...)`

```html
<template>
    <div>
        <h1>UserView<h1>

        <button @click="goHome">홈으로</button>
    </div>
</template>

<script setup>
    //router를 적용하기 위한 설정
    import {useRouter} from 'vue-router'

    const router = useRouter()

    const goHome = function(){
        router.push("/home")            // path 방식
        router.push({name: 'home'}) // name 방식
        router.push({name: 'user', params: {username: 'ssafy'}}) // 인자 넘길 때
    }
</script>

```

### router.replace()

- push 메서드와 달리 history stack에 새로운 항목을 push 하는 것이 아니라 다른 URL로 이동
- **뒤로가기가 불가능**
- 선언적 : `<RouterLink : to="" replace>`

프로그래밍적: `router.replace(...)`

### 🔍 Navigation Guard

Vue router를 통해 특정 URL에 접근할 때 다른 URL로 redirect를 하거나 취소하여 Navigation을 보호하는 역할
ex. 인증 정보가 없으면 특정 페이지에 접근 불가능(약간 인터셉터 느낌)

1. **Globally(전역 가드)**
   - 어플리케이션 전역에서 동작
   - index.js에 정의
2. **Per-route(라우터 가드)**
   - 특정 route에서만 동작
   - index.js의 각 routes에 정의
3. **In-component(컴포넌트 가드)**
   - 특정 컴포넌트에서만 동작
   - 컴포넌트 script에 정의

### Globally Guard

1. router.beforeEach()

- 다른 URL로 이동하기 직전에 실행
- to : 이동할 정보가 담긴 Route 객체
- from : 현재 URL 정보가 담긴 Route 객체
- return false : 현재 네비게이션을 취소
- return {name: 'About'} : router.push() 처럼 다른 위치로 redirect
- return 이 없으면 'to' URL Route객체로 이동
- index.js에 정의

```js
router.beforeEach((to, from) => {
  //로직
  return false;
});
```

### Per-route Guard

2. router.beforeEnter()

- route에 진입했을 때만 실행되는 함수
- 매개변수, 쿼리 값이 변경 될 때는 실행되지 않고, 다른 경로에서 탐색할 때만 실행
- 함수의 to, from 선택 반환 인자는 beforeEach와 동일
- routes 객체에 정의

### 컴포넌트 가드

3. onBeforeRouteLeave

- 현재 라우트에서 다른 라우트로 이동하기 전에 실행
- 사용자가 현재 페이지를 떠나는 동작에 대한 로직을 처리

4. onBeforeRouteUpdate

- 이미 렌더링된 컴포넌트가 같은 라우트 내에서 업데이트 되기 전에 실행
- 라우트 업데이트 시 추가적인 로직을 처리

### 🔍 Lazy Loading Routes (참고)

```js
path: '/about',
name: 'about',
component: () => import('../views/AboutView.vue')
```

- 첫 빌드시 해당 컴포넌트를 로드하지 않고, 해당 경로를 처음 방문할 때만 컴포넌트를 로드
- 앱을 빌드할 때 앱의 크기에 따라 페이지 로드 시간이 길어질 수 있기 때문에 활용

# 💡 TOPIC 7 상태관리

#### 김영섭

### 🔍 상태관리 (State Management)

- 상태(State) == 앱 구동에 필요한 Data
- 뷰(View) == 상태 선언적 매핑, 시각화 (위에서 보여주는 template)
- 기능(Action) == 사용자 Input에 따라 뷰에서 상태 변경. (function과 비슷)
- Vue 컴포넌트는 이미 반응형 상태를 관리한다.

### 🔍

### 🔍

### 🔍
