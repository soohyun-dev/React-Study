## Render and Commit

### 📌 학습 목표

<br>

- React에서 렌더링의 의미
- React가 컴포넌트를 언제, 왜 렌더링 하는지
- 화면에 컴포넌트를 표시하는 단계
- 렌더링이 항상 DOM 업데이트를 하지 않는 이유

  <br>

---

<br>

## 1단계: 렌더링 트리거

### 컴포넌트 렌더링 조건

1. 컴포넌트의 초기 렌더링일 경우
2. 컴포넌트의 state가 업데이트될 경우

- state의 상태를 업데이트하면 자동으로 렌더링 대기열에 추가됨.

  <br>

## 2단계: React 컴포넌트 렌더링

✔️ 렌더링이란

- React에서 컴포넌트를 호출하는 것.

<br>

1. 초기 렌더링에서는 React가 루트 컴포넌트를 호출한다.
2. 이후 렌더링에서 React는 state 업데이트가 일어나 렌더링을 트리거한 컴포넌트를 호출한다.

```javascript
function Something() {
  return (
    <section>
      <h1> </h1>
      <Component />
    </section>
  );
}
```

- 초기 렌더링에서 React는 `<section>`, `<h1>`, `<Component>` 태그에 대한 DOM 노드를 생성한다.

  <br>

❗렌더링은 항상 pure calculation

- 동일한 입력에는 동일한 출력.
- 이전의 state를 변경해서는 안됨.

  <br>

## 3단계: React가 DOM에 변경사항을 Commit

- 컴포넌트를 렌더링한 후 React는 DOM을 수정한다.
- React는 렌더링 간에 차이가 있는 경우에만 DOM 노드를 변경한다.

<br>

## 👨‍💻 정리

- React App의 화면 업데이트는 세 단계로 이루어진다.

1. 트리거
2. 렌더링
3. 커밋

<br>

- Strict Mode 를 사용하여 컴포넌트에서 실수를 찾을 수 있다.
- 렌더링 결과가 이전과 같다면 React는 DOM을 건드리지 않는다.
