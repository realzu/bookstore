# Adding Interactivity

**state**  
컴포넌트별 메모리  
스냅샷처럼 동작 (변수 값 바꿔도 기존 변수는 직후에 바로 변경되지 않고 리렌더링)

```javascript
setScore(score + 1);
console.log(score); // 0
```

🧚 Updating objects is state  
state의 객체/배열을 직접 변경x  
새 객체 생성 or 기존 객체의 복사본을 사용

## Responding to Events

이벤트 핸들러 함수  
Naming: `handle` 로 시작 + 뒤에는 event 이름

🧚 Inline event handlers

```jaavscript
// O: 함수 전달 (버튼 클릭시만 실행)
<button onClick={handleClick} />
// X: 함수 호출 (클릭 상관없이 '렌더링' 중에 immediately 실행)
<button onClick={handleClick()} />
```

🧚 이벤트 핸들러에 appropriate HTML Tags 사용하기  
`onClick` => div(x) button(o)

🧚 Event propagation 이벤트 전파  
실행 순서

1. 이벤트가 발생한 곳
2. 트리 '위'로 올라감

```javascript
<div onClick={() => alert("2")}>
  <button onClick={() => alert("1")}>click</button>
</div>
```

🧚 전파 & 기본 동작 막기  
이벤트 핸들러는 event object를 유일한 인자로 받음 => `e`

`e.stopPropagation()`: 이벤트가 상위 컴포넌트에 도달x  
`e.preventDefault()`: 기본 브라우저 동작 방지 (ex. form(onSubmit))

## State: A Component's Memory

지역 변수: 렌더링 발동x  
useState: 렌더링 시 데이터 유지(state), 렌더링 trigger

```javascript
import { useState } from "react";
const [something, setSomething] = useState(0); // []는 array destructuring (배열 구조분해)
```

`useState` 를 호출하는 건 -> React에게 이 컴포넌트가 무언가를 기억하길 원한다고 말하는 것!

🧚 컴포넌트에 여러 state 변수  
index, showMore 과 같은 연관없는 경우 -> 여러 state 변수 o  
but, state를 함께 자주 변경시 -> 하나로 합치기(객체 형식)

🧚 State는 isolated & private  
화면상의 특정 위치에 '지역적(local)'. state는 별도로 stored

```javascript
export default function Page() {
  return (
    // <Gallery /> 내부의 state는 각각 독립적. 두 곳에서 렌더링시 -> 각 복사본은 고유한 state를 가짐
    <div className="Page">
      <Gallery />
      <Gallery />
    </div>
  );
}
```

## Render and Commit

React의 모든 화면 업데이트는 총 3단계로 이루어진다.

> Trigger => Render => Commit

🧚 **Trigger** a render  
:: 손님의 주문을 주방에 전달  
이유) 1. 컴포넌트의 initial render 2. state(컴포넌트 or 상위요소's) 업데이트시

Initial render (첫 렌더링)
대상 노드로 `createRoot` 호출 후, `render` method 호출

```javascript
import { createRoot } from "react-dom/client";

const root = createRoot(document.getElementById("root"));
root.render(<div />);
```

🧚 React **renders** your components  
:: `Rendering` = React calling your components.  
`init`: root component 호출 (신규 DOM 노드 생성)  
`re-rendering`: 이후(subsequent renders)에는 렌더링이 trigger된 function component 호출 (변경된 properties 계산)  
(이 과정은 재귀적)  
업데이트된 컴포넌트가 다른 컴포넌트 호출 => .. => 해당 컴포넌트도 다른 컴포넌트 호출 => 화면에 표시될 컴포넌트 모두 호출할 때까지

Rendering은 same inputs & same outputs  
++ 이전 state 변경(x. 렌더링 전에 존재하는..)

🧚 React **commits** changes to the DOM  
:: 컴포넌트 렌더링 이후, 리액트는 DOM을 수정  
`init`: `appendChild()` DOM API 통해 생성한 모든 DOM 노드를 화면에 표시  
`re-rendering`: 렌더링하는 동산 계산된 것들을 적용해 DOM이 최신 렌더링 output과 일치하도록함

리액트는 렌더링간 차이 있는 경우에만 DOM 노드 변경

🧚 Browser paint  
렌더링이 끝나고 React가 DOM을 업데이트한 후, 브라우저는 화면을 다시 그린다  
`browser rendering` = `painting`
