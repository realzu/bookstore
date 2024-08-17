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
