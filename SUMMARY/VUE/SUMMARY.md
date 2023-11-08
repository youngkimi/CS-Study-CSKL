### 🔍# 💡 TOPIC 1 INTRO
#### 김병현

### 🔍

### 🔍

### 🔍

### 🔍

# 💡 TOPIC 2 Syntax1
#### 김예림, 김병현

### 🔍

### 🔍

### 🔍

### 🔍

# 💡 TOPIC 3 Syntax2
#### 석지명

### 🔍

### 🔍

### 🔍

### 🔍

# 💡 TOPIC 4 SFC
#### 김종인

### 🔍

### 🔍

### 🔍

### 🔍

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
   - 처음 로드될때 전체 페이지를 다 받아온 후에,  클라이언트 측에서 필요한 컴포넌트를 랜더링 하는 방식. 즉 페이지는 한 개이지만 링크에 따라 여러 컴포넌트를 랜더링 하여 마치 여러 페이지를 사용하는 것처럼 구성한다. 
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
- views폴더에  RouterView 위치에 렌더링 할 컴포넌트를 배치
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

import HomeView from '../views/HomeView.vue'
import AboutView from '@/views/AboutView.vue'
import UserView from '@/views/UserView.vue'

const router = createRouter({
    routes: [
        //HomeView
        {
            path: '/',
            name: 'home',
            component: HomeView
        },
        //AboutView
        {
            path: '/about',
            name: 'about',
            component: AboutView
        },
        //UserView - 동적 경로 매칭
        {
            path: '/user/:id', //매개변수 표시
            name: 'user',
            component: UserView
        }
    ]
})
```

###  UserView.vue

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
1. router.push()  -> 다른 위치로 이동
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
- 
선언적 : `<RouterLink : to="" replace>`

프로그래밍적: `router.replace(...)`

### 🔍  Navigation Guard
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
-  to : 이동할 정보가 담긴 Route 객체
-  from : 현재 URL 정보가 담긴 Route 객체
-  return false : 현재 네비게이션을 취소
-  return {name: 'About'} : router.push() 처럼 다른 위치로 redirect
-  return 이 없으면 'to' URL Route객체로 이동
-  index.js에 정의
```js
router.beforeEach((to, from) => {
    //로직
    return false
})
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