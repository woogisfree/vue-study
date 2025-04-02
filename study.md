# vue-study

## ✅ 데이터 바인딩이 필요한 이유

### 1. UI를 데이터 중심으로 만들기 위해

**전통적인 방식**

```html
document.getElementById('title').innerText = 'hello';
```

데이터가 바뀌면 직접 DOM을 찾아서 수동으로 수정해야 한다.

**Vue의 방식**

```html
<h1>{{ message }}</h1>
```

```js
data() {
  return {
    message: '안녕'
  }
}
```

message 값이 바뀌면 자동으로 화면이 업데이트가 된다. (Vue의 반응형(Reactive) 구조 덕분)

### 2. 코드의 유지보수가 쉬워짐

- 데이터와 UI 로직이 분리되어 코드가 깔끔해진다.
- 상태(state)만 바꾸면 UI는 자동으로 갱신된다.
- DOM 조작이 줄어들어 버그 가능성이 낮아진다.

### 3. 양방향 바인딩으로 폼 처리 간편화

Vue에서는 v-model을 통해 양방향 바인딩도 제공한다.

```html
<input v-model="name" />
<p>Hello, {{ name }}</p>
```

사용자 입력이 name에 반영되고 동시에 화면에도 표시된다.

## ✅ HTML 반복문

```html
<태그 v-for="작명 in 횟수" :key="작명">
<태그 v-for="(작명, i) in 메뉴들" :key="i"> {{ 작명 }}</a>
```

- 횟수 부분에 array 또는 object를 넣으면 데이터 개수만큼 반복된다.
- 소괄호 ()를 사용하면 변수 두 개를 쓸 수 있다:
  - 첫 번째 변수는 배열의 요소
  - 두 번째 변수는 인덱스 (0, 1, 2, …)

## ✅ v-on:click = @click

Vue에서 이벤트를 바인딩할 때, v-on 디렉티브의 축약형으로 `@`를 사용할 수 있다.

| 원래 문법        | 축약형       |
| ---------------- | ------------ |
| v-on:click       | @click       |
| v-on:input       | @input       |
| v-on:keyup.enter | @keyup.enter |

### 예시

```html
<button @click="handleClick">Click Me</button>
```

- `@click` 은 `v-on:click`과 완전히 동일하게 동작한다.
- Vue에서는 축약형을 더 자주 사용한다.

## ✅ 동적인 UI 만드는 법

Vue에서는 **데이터의 상태(state)** 를 기반으로 동적으로 UI를 제어할 수 있다.
모달창을 예시로 단계별로 알아보자.

### 0. HTML/CSS 로 기본 UI를 디자인한다.

먼저, 정적인 구조를 만든다.

```html
<div class="black-bg">
  <div class="white-bg">
    <h4>상세페이지임</h4>
    <p>상세페이지내용임</p>
  </div>
</div>
```

### 1. UI의 현재 상태를 데이터로 저장한다.

이 UI 요소가 보일지 말지를 데이터로 관리한다.

```js
data() {
    return {
      모달창열렸니: false,
    };
  },
```

`모달창열렸니`는 boolean 타입으로 모달의 열림/닫힘 상태를 표현한다.

### 2. 데이터에 따라 UI가 보일지 말지를 조건부 렌더링한다.

`v-if`를 사용해 조건에 따라 해당 요소를 보여주거나 숨길 수 있다.

```html
<div class="black-bg" v-if="모달창열렸니">
  <div class="white-bg">
    <h4>상세페이지임</h4>
    <p>상세페이지내용임</p>
  </div>
</div>
```

### 3. 이벤트를 통해 상태를 바꿔 UI를 제어한다.

버튼이나 텍스트 클릭 등을 통해 `모달창열렸니` 값을 변경하면 자동으로 UI도 변경된다.

```html
<h4 @click="모달창열렸니 = true">{{ products[0] }}</h4>
```

클릭 이벤트를 통해 모달창이 열리도록 제어할 수 있다.

## ✅ v-if / v-else-if / v-else 문법

Vue에서는 조건에 따라 HTML 요소를 보여줄지 말지를 결정할 때 `v-if`, `v-else-if`, `v-else` 를 사용한다.

### v-if

조건이 `true`일 때만 해당 요소를 **렌더링**한다.

```html
<p v-if="isLoggedIn">Welcome!</p>
```

### v-else-if

앞선 v-if가 false일 때, 대체 조건을 검사한다. (일종의 else if)

```html
<p v-if="score >= 90">A score</p>
<p v-else-if="score >= 80">B score</p>
<p v-else-if="score >= 70">C score</p>
```

### v-else

위의 v-if, v-else-if 조건이 모두 false일 경우 실행된다.

```html
<div v-if="age > 19">You are an adult.</div>
<div v-else-if="age > 13">You are a teenager.</div>
<div v-else>You are a child.</div>
```

## ✅ v-if vs v-show 차이점

Vue에서는 조건부 렌더링을 위해 `v-if`와 `v-show` 두 가지를 제공한다.
이 둘은 비슷해 보이지만 동작 방식이 다르다.

### 1. 공통점

- 둘 다 조건이 true일 때만 DOM 요소를 화면에 표시한다.

### 2. 차이점

| 항목             | `v-if`                                    | `v-show`                                            |
| ---------------- | ----------------------------------------- | --------------------------------------------------- |
| 렌더링 방식      | 조건이 true일 때 **DOM 자체를 생성/제거** | DOM은 항상 있음. 대신 **`display: none`** 으로 숨김 |
| 초기 렌더링 비용 | 낮음 (필요할 때만 생성)                   | 높음 (무조건 렌더링되고 숨김 처리됨)                |
| 토글 비용        | 높음 (DOM을 계속 붙였다 떼야 함)          | 낮음 (CSS 속성만 바꾸면 됨)                         |
| 사용 예시        | 조건이 자주 바뀌지 않는 경우              | 조건이 자주 바뀌는 경우                             |

### 예시

```html
<!-- v-if 예제 -->
<p v-if="visible">이건 v-if로 보이는 문장입니다.</p>

<!-- v-show 예제 -->
<p v-show="visible">이건 v-show로 보이는 문장입니다.</p>
```

## ✅ export / import 문법

어떤 javascript 파일에서 만든 **변수, 함수, 객체** 등을 다른 파일에서 **재사용**하고 싶을 때 사용하는 문법이다.

### export default / import

```js
// oneroom.js
var apple = 10;
export default apple;
```

```js
// App.vue 또는 다른 파일
import 작명 from './oneroom.js'; // 작명 자유
console.log(작명); // 10
```

- export default는 한 파일에 단 1번만 사용 가능
- import할 때는 작명 자유

### export {} / import {}

```js
// oneroom.js
var apple = 10;
var apple2 = 100;

export { apple, apple2 };
```

```js
// App.vue 또는 다른 파일
import { apple, apple2 } from './oneroom.js';

console.log(apple); // 10
console.log(apple2); // 100
```

- export는 원하는 만큼 여러 번 사용 가능
- import 할 때는 내보낸 이름과 똑같이 써야함

## ✅ 컴포넌트(Component)

- Vue 컴포넌트는 **UI를 재사용 가능한 단위로 나눈 조각**이다.
- 하나의 컴포넌트는 자체적인 **HTML, CSS, JavaScript**를 포함할 수 있고, 이들을 조합해 복잡한 UI를 구성한다.

### 컴포넌트를 사용하는 이유

- UI를 재사용할 수 있다.
- 코드가 읽기 쉽고 유지보수가 쉬워진다.
- 상태(state), 이벤트, 로직 등을 **각각의 컴포넌트 내부에서 독립적으로 관리**할 수 있다.

### 컴포넌트의 기본 구조

```html
<!-- MyComponent.vue -->
<template>
  <div>
    <h2>{{ message }}</h2>
  </div>
</template>

<script>
  export default {
    name: 'MyComponent',
    data() {
      return {
        message: 'Hello from component!',
      };
    },
  };
</script>

<style scoped>
  h2 {
    color: blue;
  }
</style>
```

- `<template>`: 화면에 보여질 HTML 구조
- `<script>`: 컴포넌트의 로직, 상태(data), 메서드 등
- `<style scoped>`: 해당 컴포넌트에만 적용되는 CSS

### 컴포넌트 등록 & 사용 방법

#### 1. 컴포넌트 등록 (App.vue 등)

```html
<script>
  import MyComponent from './components/MyComponent.vue';

  export default {
    components: {
      MyComponent,
    },
  };
</script>
```

#### 2. 템플릿에서 사용

```html
<template>
  <div>
    <MyComponent />
  </div>
</template>
```

### 컴포넌트의 종류

#### 1. 전역 컴포넌트

Vue 애플리케이션 전체에서 사용할 수 있는 컴포넌트

```js
import Vue from 'vue';
import MyComponent from './MyComponent.vue';

Vue.component('MyComponent', MyComponent);
```

#### 2. 로컬 컴포넌트

특정 컴포넌트 파일 내에서만 사용하는 컴포넌트

```js
export default {
  components: {
    MyComponent,
  },
};
```

## ✅ Props

Vue에서 `props`란 **부모 컴포넌트가 자식 컴포넌트에게 데이터를 전달할 때 사용하는 문법**이다.

### 언제 사용하나?

- 어떤 데이터를 여러 컴포넌트에서 공유해야 할 때
- 특히 자식 컴포넌트에서 부모의 데이터를 **읽기 전용**으로 사용하고 싶을 때
- 데이터를 다른 컴포넌트에서 복사해서 쓰면 안되는 이유는, 데이터가 변경되었을 때 복사본끼리 동기화가 불가능하기 때문이다.

### 용어 정리

| 용어          | 의미                               |
| ------------- | ---------------------------------- |
| 부모 컴포넌트 | 상위 컴포넌트 (예: App.vue)        |
| 자식 컴포넌트 | 하위 컴포넌트 (예: Modal.vue 등)   |
| props         | 부모가 자식에게 보내는 데이터 통로 |

### props 사용 방법

#### 1. 부모 -> 자식에게 데이터 보내기

```html
<!-- APP.vue -->
<Modal : 원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니" />
```

- :는 데이터 바인딩의 약어이며 동시에 props 전달 기능도 수행한다.
- `작명="데이터이름"` 형식이다.
- 데이터 전송 예시

  ```html
  <!-- Array 전송 -->
  <Discount :data="[1, 2, 3]" />

  <!-- Object 전송 -->
  <Discount :data="{ age: 20 }" />

  <!-- 숫자 100 전송 -->
  <Discount :data="100" />

  <!-- 문자열 "100" 전송 -->
  <Discount data="100" />

  <!-- 문자 전송 (콜론 없으면 문자열로 인식) -->
  <Discount data="안녕하쇼" />
  ```

#### 2. 자식 컴포넌트에서 props 등록하기

```js
// Modal.vue
export default {
  name: 'Modal',
  props: {
    원룸들: Array,
    누른거: Number,
    모달창열렸니: Boolean,
  },
};
```

- props 객체에 데이터 이름과 타입을 정의
- 타입 예시: Array, Object, String, Number, Boolean 등

#### 3. props 데이터 사용하기

```html
<!-- Modal.vue -->
<img :src="원룸들[누른거].image" />
<h4>{{ 원룸들[누른거].title }}</h4>
```

- props로 받은 데이터는 data()에 없어도 바로 바인딩 가능하다.
- 마치 data처럼 template 안에서 자유롭게 사용 가능하다.
