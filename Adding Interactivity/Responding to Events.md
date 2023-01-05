## Responding to Events

### 📌 학습 목표

<br>

- 이벤트 핸들러를 작성하는 다양한 방법을 안다.
- 부모 구성 요소에서 이벤트 처리를 전달하는 방법을 안다.
- 이벤트 전파와 중지 방법을 안다.
  <br>

---

### ✔️ 이벤트 핸들러

<br>

- 보통은 컴포넌트 내부에 정의된다.
- 이름은 `handle` 이라는 이름으로 시작하고, 이벤트 효과에 받는 이름을 붙여준다.
  <br>

```javascript
(onClick = { handleClick }), (onMouseEnter = { handleMouseEnter });
```

<br>

- 이렇게 간단하게 JSX 인라인으로 작성도 가능하다.

```javascript
<button onClick={function handleClick() {
    alert('clicked!');
}}>
```

<br>

- 주의할 점은 이벤트 핸들러에 전달하는 함수는 호출하는 것이 아닌 말 그대로 전달만 해야한다.

```javascript
<button onClick={handleClick()}>  // ❌
```

<br>

### 이벤트 핸들러 props 이름 짓기

<br>

- 이름은 `on` 이라는 이름으로 시작하고 대문자 문자로 이어준다.

```javascript
onClick;
```

<br>

### 이벤트 전파

<br>

- 이벤트 핸들러는 컴포넌트가 가지는 모든 하위 이벤트들도 캡쳐한다.
- 하위 이벤트는 발생하면 위로 '전파' 또는 '버블' 된다라고 말하게 되는데, 이는 발생한 위치에서 시작하여 트리 위로 올라가는 것이다.
- 하단 코드의 버튼을 누르게 되면 `이벤트 발생` 알림이 뜨고 이어서 `이벤트 버블링` 알림도 뜨게 된다.

```javascript
<div
  onClick={() => {
    alert("이벤트 버블링");
  }}
>
  <button onClick={() => alert("이벤트 발생")}> 버튼 </button>
</div>
```

<br>

### 이벤트 전파 중지

<br>

- 이벤트가 부모 컴포넌트에 도달하는 것을 방지하려면 `e.stopPropagation()` 을 호출해야 한다.
- 하단 코드의 버튼을 누르면 `이벤트 발생` 알림만 뜬다.

```javascript
function Button({ onClick, children }) {
  return (
    <button
      onClick={(e) => {
        e.stopPropagation();
        onClick();
      }}
    >
      {children}
    </button>
  );
}

<div
  onClick={() => {
    alert("이벤트 버블링");
  }}
>
  <Button onClick={() => alert("이벤트 발생")}> 버튼 </Button>
</div>;
```

<br>

❗주의할점

#### e.stopPropagation()

- 상위 태그에 연결된 이벤트 핸들러의 실행을 중지시킨다.
- 이벤트가 상위 엘리먼트에 전달되는 것을 막아준다.

<br>

#### e.preventDefault()

- 이벤트 태그의 고유 동작들을 막아준다.
- 브라우저 고유의 동작을 중단시켜주는 역할

<br>

---

<br>

### 👨‍💻 정리

<br>

- 함수를 props로 전달하여 이벤트 처리를 할 수 있다.
- 이벤트 핸들러는 호출시키는 것이 아닌 전달해야 한다.
- 이벤트 핸들로 함수를 인라인으로 정의할 수 있음.
- 부모에서 자식으로 이벤트 핸들러 props를 정의할 수 있다.
- 이벤트는 위쪽으로 전달됨. 이것을 방지하려면 e.stopPropagation()을 호출하자.
- 원치않는 기본 브라우저 동작은 e.preventDefault()를 호출하자.

<br>
