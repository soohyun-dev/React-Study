## Queueing a Series of State Updates

### 📌 학습 목표

- 일괄처리가 무엇인지 그리고 React가 이를 사용하여 여러 state를 업데이트하는 방법
- 한 행에서 동일한 상태 변수에 여러 업데이트를 적용하는 방법

<br>

---

```javascript
import { useState } from "react";

export default function Counter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h1>{number}</h1>
      <button
        onClick={() => {
          // 버튼 클릭시 1만 증가됨.
          setNumber(number + 1);
          setNumber(number + 1);
          setNumber(number + 1);
        }}
      >
        +3
      </button>
    </>
  );
}
```

React는 state를 업데이트 하기 전에 이벤트 핸들러의 모든 코드가 실행될 때까지 기다립니다.
이 이유로 모든 setNumber() 가 호출 된 이후에 다시 렌더링이 발생하는 이유입니다.

- React는 클릭과 같은 여러 의도적인 이벤트를 일괄 처리하지 않고 개별적으로 처리합니다.

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
          // 버튼 클릭시 3 증가
          setNumber((n) => n + 1);
          setNumber((n) => n + 1);
          setNumber((n) => n + 1);
        }}
      >
        +3
      </button>
    </>
  );
}
```

<br>

- state 값을 단순히 교체하는 대신 state 값으로 무언가를 수행하도록 지시
- `n => n+1`은 업데이트 함수.

- 0 + 1 = 1
- 1 + 1 = 2
- 2 + 1 = 3

- React는 최종 결과로 3을 저장하고 useState에서 반환

```javascript
import { useState } from "react";

export default function Counter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h1>{number}</h1>
      <button
        onClick={() => {
          // 42로 변경
          setNumber(number + 5);
          setNumber((n) => n + 1);
          setNumber(42); // 앞에 계산 값무시하고 42로 return 되기 때문.
        }}
      >
        Increase the number
      </button>
    </>
  );
}
```

<br>

## 👨‍💻 정리

- state를 설정하면 기존 렌더링의 변수가 변경되지 않고 새로운 렌더링 요청
- React는 이벤트 핸들러 실행이 완료된 후 state 업데이트를 처리. 이를 일괄 처리라고 함.
- 하나의 이벤트에서 일부 상태를 여러 번 업데이트하려면 `setNumber(n => n+1)`와 같은 업데이트 기능을 사용하자.
