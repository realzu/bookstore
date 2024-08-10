# Describing the UI

## Conditional Rendering

- `&&` 왼쪽에 숫자를 두지 않기

숫자를 두게 된다면, 좌측을 boolean 으로 만들기  
또는 `!!` 이중 부정 사용하여 falsy => false 처리

```javascript
const messageCount = 0;
return (
    messageCount && <p>New messages</p>
) // return 0
// messageCount > 0 // false
// !!messageCount // false
```

## Rendering Lists

- 화살표 함수는 `=>` 뒤에 식 반환 (`return` 필요 x)

but, 뒤에 `{}` curly brace => `return` 필요

```javascript
const listItems = ['a', 'b'].map((item, i) => <p key={i}>{item}</p>)
```

- key

필요한 이유: 재정렬시 위치가 변경되더라도, key를 통해 식별 가능  
key =>  string or number type  
배열의 index를 사용하면, 배열 순서 변경시 버그 발생할 수도 있음  
Math.random (X) => 렌더링시마다 매번 컴포넌트와 DOM 재생성  
하위 리스트 아이템을 컴포넌트로 만들 경우, 컴포넌트 자체에 key로 줌
```javascript
<Profile key={id} userId={id} />
```