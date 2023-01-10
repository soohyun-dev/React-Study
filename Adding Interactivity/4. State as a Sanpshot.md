## State as a Snapshot

### 📌 학습 목표

- state 설정이 어떻게 다시 렌더링을 실행하는지
- 언제 그리고 어떻게 state가 업데이트되는가
- state를 설정한 후에 왜 state 값이 즉시 업데이트 되지 않는가
- 이벤트 핸들러가 state의 "snapshot"에 어떻게 접근하는가

  <br>

---

### state를 설정하면 렌더링을 실행

- 인터페이스가 이벤트에 반응하려면 State를 업데이트해야함.

<br>

### 렌더링은 적시에 스냅샷을 생성

- "렌더링"은 React가 함소 컴포넌트를 호출하는 것을 의미.

<br>

React가 컴포넌트를 다시 렌더링할 때,

1. React가 함수를 다시 호출
2. 함수가 새 JSX 스냅샷을 반환
3. React는 반환된 스냅샷을 일치하도록 화면을 업데이트

- 컴포넌트의 메모리인 state는 함수가 반환된 후 사라지는 일반 변수와는 다르다. 컴포넌트 자체에서 살아있는 것 같은 값이 'State' 이다.

```javascript
// 초기값 number = 0;

<button
  onClick={() => {
    setNumber(number + 1);
    setNumber(number + 1);
    setNumber(number + 1);
  }}
>
  +3
</button>
```

- 위 예시 코드는 버튼을 눌렀을때 마치 setNumber가 세번 실행되어 3이 증가될 것이라는 예측을 불러 일으킨다.
- 하지만, 실제로 버튼을 눌러보면 1씩 증가하게 된다.
- 이는 렌더링의 이벤트 핸들러에서 `number` 값은 항상 `0` 이므로 0에 +1을 하는 작업이 세번 이루어지기 때문이다.

<br>

```javascript
import { useState } from "react";

export default function Counter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h1>{number}</h1>
      <button
        onClick={() => {
          setNumber(number + 5);
          setTimeout(() => {
            alert(number);
          }, 3000);
        }}
      >
        +5
      </button>
    </>
  );
}

// +5 한 값이 alert 되는 것이 아닌 이전 값이 alert 된다.
```

<br>

- 이벤트가 비동기적으로 처리된다 할지라도 state 값은 렌더링 내에서 절대 변하지 않는다.
- 이는 React가 컴포넌트를 호출하여 UI의 스냅샷을 찍은 값이 고정된 것과 같은 현상이다.
- 아무리 지연을 시킬려하여도 이벤트 핸들러가 호출될 당시의 값이 state의 고정값으로 유지된다.

<br>

## 👨‍💻 정리

- state를 설정하면 리렌더링이 요청된다.
- React는 컴포넌트 외부에 state를 저장한다.
- `useState`를 호출하면 React는 렌더링의 state에 대한 스냅샷을 제공한다.
- 모든 렌더링 혹은 그 안의 함수는 항상 React가 렌더링에 부여한 state의 스냅샷을 참조할 것이다.
- 과거에 생성된 이벤트 핸들러는 생성되었을 당시 렌더링의 state 값을 가진다.
