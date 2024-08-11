# Describing the UI

## Conditional Rendering

- `&&` 왼쪽에 숫자를 두지 않기

숫자를 두게 된다면, 좌측을 boolean 으로 만들기  
또는 `!!` 이중 부정 사용하여 falsy => false 처리

```javascript
const messageCount = 0;
return messageCount && <p>New messages</p>; // return 0
// messageCount > 0 // false
// !!messageCount // false
```

## Rendering Lists

- 화살표 함수는 `=>` 뒤에 식 반환 (`return` 필요 x)

but, 뒤에 `{}` curly brace => `return` 필요

```javascript
const listItems = ["a", "b"].map((item, i) => <p key={i}>{item}</p>);
```

- key

필요한 이유: 재정렬시 위치가 변경되더라도, key를 통해 식별 가능  
key => string or number type  
배열의 index를 사용하면, 배열 순서 변경시 버그 발생할 수도 있음  
Math.random (X) => 렌더링시마다 매번 컴포넌트와 DOM 재생성  
하위 리스트 아이템을 컴포넌트로 만들 경우, 컴포넌트 자체에 key로 줌

```javascript
<Profile key={id} userId={id} />
```

## Keeping Components Pure

- Components as formulas
  - 함수/컴포넌트 호출 전에 존재했던 객체/변수 변경x
  - 동일 input -> output

컴포넌트는 props에 의존하므로써 순수  
StrictMode => 2번씩 실행하기에 output이 다르게 나오는 컴포넌트 찾는 데에 도움

- side effects
  - functional programming은 순수성 의존하지만, 화면 업데이트/애니메이션/데이터 변경 등 무언가 바뀌어야 함 = "사이드 이펙트"
  - 사이드 이펙트는 주로 event handlers
  - `event handler` = 액션이 일어났을 때 React가 실행하는 함수
  - 이벤트 핸들러에 적합한 게 없다면 최후는 `useEffect`

Rendering can happen "at any time", -> so, 컴포넌트들은 서로의 렌더링 순서에 의존x

1. JSX에 최대한 컴포넌트 로직을 표현하며
2. "change things" 필요 시 `event handler` 사용
3. `useEffect`는 최후의 수단
