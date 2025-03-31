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

예시

```html
<button @click="handleClick">Click Me</button>
```

- `@click` 은 `v-on:click`과 완전히 동일하게 동작한다.
- Vue에서는 축약형을 더 자주 사용한다.
