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

## ✅ emit

- Vue에서는 자식 컴포넌트가 부모 컴포턴트의 데이터를 직접 변경할 수 없다.
- `props`로 전달된 데이터는 읽기 전용이기 때문에 변경하면 vue가 경고를 띄운다.
- 그래서 부모 컴포넌트의 데이터를 변경하려면, 자식 컴포넌트는 `$emit()` 메서드를 통해 부모 컴포넌트에게 데이터를 변경해달라고 요청해야한다. 이를 **커스텀 이벤트(Custom Event)** 라고 한다.

### $emit 사용법 (자식 컴포넌트가 부모 컴포넌트에게 데이터 전달)

```html
<!-- 자식 컴포넌트 : openModal 이라는 커스텀 이벤트를 부모에게 전송 -->
<h4 @click="$emit('openModal')">제목</h4>

<!-- 부모 컴포넌트 : 자식이 보낸 openModal 이벤트를 수신해서 원하는 동작 실행 -->
<Card @openModal="모달창열렸니 = true" />
```

#### $emit 으로 자료 전달도 가능하다.

```html
<!-- 자식 컴포넌트 -->
<h4 @click="$emit('openModal', 원룸.id)">제목</h4>
```

- `$emit('이벤트명', 전달할 자료)` 형태
- 두 번째 인자로 어떤 값이든 보낼 수 있음 (숫자, 문자열, 객체 등)

```html
<Card @openModal="모달창열렸니 = true; 누른거 = $event" />
```

- `$event`는 자식이 보낸 두 번째 인자값

#### 메서드 안에서도 사용 가능하다.

```js
<template>
  <h4 @click="클릭시()">제목</h4>
</template>

<script>
export default {
  methods: {
    클릭시() {
      this.$emit('openModal', this.원룸.id);
    }
  }
}
</script>
```

## ✅ 사용자 입력 처리 및 v-model 정리

Vue에서는 `<input>`, `<textarea>`, `<select>` 등의 입력 요소에서 사용자가 입력한 값을 `data()`에 저장하고, 이를 이용해 동적인 UI를 만들 수 있다.

### 1. 입력값을 `data`에 저장하는 기본 방식

```html
<input @input="month = $event.target.value" />
```

- @input: 사용자가 값을 입력할 때마다 실행되는 이벤트
- $event: 이벤트 객체 (javascript의 e와 같음)
- $event.target.value: input 태그 안의 값
- month: data()에 정의된 변수. 여기에 값이 실시간으로 저장됨

```js
data() {
  return {
    month: 0
  }
}
```

### 2. 총 가격 계산 기능 예시

```html
<p>총 가격: {{ month * 원룸들[누른거].price }}원</p>
```

- 사용자가 month에 입력한 숫자에 따라 총 가격이 자동으로 계산됨

### 3. 더 간단한 방식: v-model

```html
<input v-model="month" />
```

- v-model은 `@input + :value`를 합친 문법
- 데이터 바인딩과 이벤트 핸들링을 동시에 처리
- 입력값이 data.month에 자동으로 저장됨

### 4. 숫자로 자동 변환: v-model.number

```html
<input v-model.number="month" />
```

- 사용자가 "123"을 입력하면 "123" -> 123 으로 자동 변환해 저장
- 기본적으로 `<input>` 입력값은 모두 문자열로 들어오기 때문에 숫자 처리할 때는 .number modifier 사용

### 5. 다른 요소에서도 사용 가능

| 태그 종류                 | 설명                             |
| ------------------------- | -------------------------------- |
| `<textarea>`              | 긴 텍스트 입력 필드              |
| `<select>`                | 드롭다운 옵션                    |
| `<input type="checkbox">` | true/false 값을 바인딩할 때 유용 |
| `<input type="radio">`    | 라디오 버튼 그룹                 |

### 예시 전체 코드 (Modal.vue 일부)

```html
<template>
  <div>
    <input v-model.number="month" />
    <p>총 가격: {{ month * 원룸들[누른거].price }}원</p>
  </div>
</template>

<script>
  export default {
    props: ['원룸들', '누른거'],
    data() {
      return {
        month: 1,
      };
    },
  };
</script>
```

## ✅ 사용자 입력값 감시 및 유효성 검사

### watch

watch는 특정 데이터를 실시간으로 감시하면서, 값이 바뀔 때마다 특정 코드를 실행할 수 있다.

```js
export default {
  data() {
    return {
      month: 1,
    };
  },
  // watch: { 감시할데이터() {} } - 감시할데이터가 변경될 때마다 watcher 실행됨
  watch: {
    month(newVal, oldVal) {
      // month가 바뀔 때마다 실행
    },
  },
};
```

- newVal: 변경된 값
- oldVal: 변경되기 전 값

### 예시

```js
// 1. 문자 입력시 경고 띄우고 초기화
watch: {
  month(val) {
    if (isNaN(val)) {
      alert('숫자만 입력해주세요!');
      this.month = 1;
    }
  }
}

// 2. 특정 범위를 벗어나면 경고
watch: {
  month(val) {
    if (val > 12) {
      alert('최대 12개월까지만 가능합니다.');
      this.month = 12;
    }
  }
}
```

### 더 복잡한 검사는?

Vue에서는 간단한 검사는 watch로 충분하지만, 이메일 형식, 비밀번호 복잡도, 체크박스 필수 확인 등 조건이 많아질 경우 `form validation 라이브러리`를 사용하는 걸 권장한다.

**대표적인 라이브러리**

| 라이브러리     | 특징                                                 |
| -------------- | ---------------------------------------------------- |
| `vee-validate` | Vue 전용 검증 라이브러리                             |
| `vuelidate`    | 컴포지션 API 친화적                                  |
| `yup`          | 다양한 검증 스키마 지원(vee-validate와 함께 자주 씀) |

## ✅ UI 등장/퇴장시 애니메이션 주는 방법

Vue에서는 화면에 등장하거나 사라지는 요소에 부드러운 애니메이션 효과를 줄 수 있다.

### 방법1. 순수 CSS로 애니메이션 주기

1. 애니메이션 시작 전 class 디자인
2. 애니메이션 동작 후 class 디자인
3. 조건에 따라 애니메이션 동작 후 class 부착

```html
<div :class="{ '클래스명': 조건 }"></div>
```

4. 시작 전 class 명에 transition 속성을 주면 부드러운 애니메이션 효과 완성

```html
<template>
  <!-- 모달창열렸니 가 true 일때만 .end 부착 -->
  <div class="start" :class="{ end : 모달창열렸니 }">
    <Modal
      @closeModal="모달창열렸니 = false"
      :원룸들="원룸들"
      :누른거="누른거"
      :모달창열렸니="모달창열렸니"
    />
  </div>
</template>

<style>
  .start {
    opacity: 0;
    transition: all 1s;
  }

  .end {
    opacity: 1;
  }
</style>
```

### 방법2. Vue에서 제공하는 `<Transition>` 태그 사용

Vue가 제공하는 `<Transition>` 태그를 사용하면 UI 등장/퇴장시 애니메이션을 자동으로 처리할 수 있다.

1. `<Transition name="작명">` 태그로 UI를 감싼다.
2. 해당 name 기반으로 CSS 클래스를 정의한다.

| 단계                 | 클래스명           |
| -------------------- | ------------------ |
| 등장 시작 전         | .작명-enter-from   |
| 등장 중(transaition) | .작명-enter-active |
| 등장 완료 후         | .작명-enter-to     |
| 퇴장 시작 전         | .작명-leave-from   |
| 퇴장 중              | .작명-leave-active |
| 퇴장 완료 후         | .작명-leave-to     |

예시

```html
<template>
  <Transition name="fade">
    <Modal
      @closeModal="모달창열렸니 = false"
      :원룸들="원룸들"
      :누른거="누른거"
      :모달창열렸니="모달창열렸니"
    />
  </Transition>
</template>

<style>
  .fade-enter-from {
    opacity: 0;
  }
  .fade-enter-active {
    transition: all 1s;
  }
  .fade-enter-to {
    opacity: 1;
  }

  .fade-leave-from {
    opacity: 1;
  }
  .fade-leave-active {
    transition: all 1s;
  }
  .fade-leave-to {
    opacity: 0;
  }
</style>
```

## ✅ 상품 목록 정렬

Vue에서는 `v-for`로 출력된 배열이 변경되면 화면도 변경되므로, 데이터만 정렬하면 된다.

### 1. `.sort()`로 가격순 정렬하기

원룸들 데이터 구조

```js
원룸들 = [
  { title: 'room1', price: 30000 },
  { title: 'room2', price: 40000 },
  ...
]
```

**정렬 버튼과 메서드**

```html
<button @click="priceSort">가격순 정렬</button>
```

```js
methods: {
  priceSort() {
    this.원룸들.sort(function(a, b) {
      return a.price - b.price; // 오름차순
      // return b.price - a.price 내림차순
    });
  }
}
```

- a, b는 배열 내의 객체 두 개를 비교하는 역할
- return 값 기준 정리
  | return 값 | 의미 | 결과 정렬 순서 |
  | --------- | ------------------- | -------------- |
  | 음수 | a < b -> a가 앞으로 | a, b |
  | 양수 | a > b -> b가 앞으로 | b, a |
  | 0 | 순서 그대로 유지 | 그대로 |

**등호(=) 로 복사하면 안되는 이유**

```js
this.원룸들오리지널 = this.원룸들; // ❌
```

- 이렇게 하면 값 복사가 아니라 **참조 공유**가 발생함
- this.원룸들을 정렬하면 this.원룸들오리지널도 함께 정렬됨
- 즉, 복사한 게 아니라 같은 데이터를 가리키게 됨
- 자료형이 `숫자, 문자`인 경우 등호는 값을 복사하고, 자료형이 `배열, 객체`인 경우에는 참조 복사가 일어남

**진짜 복사 방법: 스프레드 문법**

```js
this.원룸들 = [...this.원룸들오리지널]; // 안전한 복사
```

- 스프레드 문법은 배열 안의 요소를 펼쳐서 다시 닫는 방식
- 배열을 **해체**한 뒤, 새로운 배열로 **재조립**하는 느낌
- 그래서 기존 배열과 값 공유 없이 별개의 배열이 됨

### 2. 되돌리기 버튼

```html
<button @click="sortBack">되돌리기</button>
```

```js
data() {
  return {
    원룸들: [...data], // 화면에 보일 데이터
    원룸들오리지널: [...data], // 원본 저장용
  }
},
methods: {
  sortBack() {
    this.원룸들 = [...this.원룸들오리지널]; // 스프레드로 안전하게 복사
  }
}
```

## ✅ Lifecycle Hook

- Vue 컴포넌트는 생성되고, 화면에 보여지고, 데이터가 바뀌고, 사라지는 일련의 과정을 거친다.
- 이 과정을 Lifecycle(생명주기)라고 하며, 각 단계에서 실행할 수 있는 특별한 메서드를 **Lifecycle Hook**이라고 부른다.

### Lifecycle 의 주요 단계

1. Creation (생성)
2. Mounting (DOM 장착)
3. Updating (재랜더링)
4. Unmounting (제거)

### 주요 Lifecycle Hook 목록

| Hook              | 실행 시점                                            |
| ----------------- | ---------------------------------------------------- |
| `beforeCreate()`  | 인스턴스 생성 직전, `data`, `methods` 아직 준비 안됨 |
| `created()`       | 인스턴스 생성 후, `data`, `methods` 접근 가능        |
| `beforeMount()`   | 템플릿이 실제 DOM에 장착되기 직전                    |
| `mounted()`       | DOM에 컴포넌트가 완전히 삽입된 직후                  |
| `beforeUpdate()`  | 반응형 데이터가 변경되어 DOM 업데이트 직전           |
| `updated()`       | DOM이 다시 렌더링된 직후                             |
| `beforeUnmount()` | 컴포넌트가 제거되기 직전                             |
| `unmounted()`     | 컴포넌트가 제거된 직후                               |

예시

```js
export default {
  data() {
    return {
      message: 'Hello Vue!',
    };
  },
  created() {
    console.log('데이터와 메서드가 준비되었습니다.');
  },
  mounted() {
    console.log('컴포넌트가 화면에 렌더링되었습니다.');
  },
  beforeUpdate() {
    console.log('데이터가 변경되어 DOM이 업데이트 되기 전입니다.');
  },
  updated() {
    console.log('DOM이 업데이트 되었습니다.');
  },
  beforeUnmount() {
    console.log('컴포넌트가 곧 제거됩니다.');
  },
  unmounted() {
    console.log('컴포넌트가 제거되었습니다.');
  },
};
```
