# state 업데이트

리액트는 상태 업데이트 스케쥴을 갖고 있어서 바로 실행하지 않는다.

그래서 이론적으로 동시에 수많은 상태 업데이트를 계획한다면

오래되었거나 잘못된 상태에 의존할 수도 있다. 

스냅샷 ⇒ state 상태 

```jsx
setUserInput({
  ...userInput,
  enteredTitle: event.target.value,
});
```

👇

```jsx
setUserInput((prevState) => {
  return { ...prevState, enteredTitle: event.target.value };
});
```

setUserInput 함수에서 상태값을 받아와 가장 최신 상태의 값이라는 것과 항상 계획된 상태 업데이트를 염두에 두고 있다는 것을 보장한다.

 → 이것은 항상 최신 상태의 스냅샷에서 작업하도록 하는 좀 더 안전한 방법이다.

이전 상태에 따라 상태를 업데이트할 때마다 이러한 함수 구문을 사용해야 한다.

→ 상태 업데이트가 이전 상태에 의존하고 있다면 이 구문을 사용할 것!!