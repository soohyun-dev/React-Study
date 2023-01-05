## State

### 📌 학습 목표

<br>

- useState Hook에 state를 추가하는 법
- useState Hook이 return 하는 값의 쌍
- 하나 이상의 state 변수를 추가하는 법
- state가 왜 local로 불리는가

<br>

---

<br>

### useState

<br>

```javascript
const [index, setIndex] = useState(0);
```

<br>

- index는 state 변수다.
- setIndex는 setter 함수이다.
  <br>

  동작법

```javascript
function handleClick() {
  setIndex(index + 1);
}
```

<br>

React에서 'use'로 시작하는 함수를 Hook 이라고 한다.

Hook은 React가 렌더링하는 동안에만 사용할 수 있는 특수한 기능이다.

<br>

### 컨벤션

- setter 함수에는 state변수 앞에 set을 붙이는 형식으로 이름을 짓는다.
- useState argument로는 state 초깃값을 준다.

```javascript
const [something, setSomething] = useState(0);
```

<br>

### useState 동작 방식

```javascript
const [index, setIndex] = useState(0);
```

<br>

1. 컴포넌트 렌더링
2. index 변수에 초기값 `0` 전달.
3. [0, setIndex] return
4. state update => `setIndex(1)`
5. 변한 state값 기억
6. 컴포넌트 리렌더링
7. [1, setIndx] return
   <br>

### State는 독립적이다.

- state는 독립적이고 private하다.
- state는 컴포넌트 인스턴스에 대해 독립적이다.
- state는 각 컴포넌트에서 독립적인 형태로 존재하여 컴포넌트간의 영향을 서로 주거나 받지 않는다.

<br>

---

<br>

## 👨‍💻 정리

<br>

- 컴포넌트가 렌더링 도중 일부 정보를 기억해야 하는 경우 state를 사용한다.

- state 변수는 useState Hook의 호출을 통해 선언됨.

- useState는 현재 state 값과 이를 Update할 함수의 값 쌍을 반환한다.

- state 변수는 하나 이상 선언할 수 있고 React 내부적으로 순서대로 일치시킨다.

- State는 컴포넌트에 대해 독립적이다. 두 곳에서 렌더링 된 state 각각 고유한 상태를 가진다.
