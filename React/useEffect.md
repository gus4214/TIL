# useEffect

React.js에서 가장 멋진 점은 component를 **새로고침** 한다는 것이다.
<br/>
😄 새로운 데이터가 들어올 때 마다 refresh 한다는 것 → 우리가 직접 refresh 해도 되지 않아서 좋다.

🤔 하지만 가끔 component가 **처음 render** 될 때만 코드가 실행되길 원할 수 있다.

```jsx
function App() {
  const [counter, setValue] = useState(0);
  const onClick = () => setValue((prev) => prev + 1);
  console.log("hi there");
  return (
    <div>
      <h1 className={styles.title}>Welcome back!!!</h1>
      <Button text={"Continue"} />
      <h1>{counter}</h1>
      <button onClick={onClick}>click me</button>
    </div>
  );
}
```

위의 코드에서는 state가 변할 때마다 매번 `console.log(”hi there”)`가 실행된다.

👉 state가 변화할 때 나의 모든 `component` / `code`는 다시 실행 된다.

하지만 그것을 원하지 않고 첫번째 render에만 실행되고, 다른 state변화에는 실행되지 않도록 실행되길 원할 수 있다.

ex) API를 통해 데이터를 가져올 때

- 첫번째 component render에서 API를 call 하고,
- 이후 state가 변화할 때, 그 API에서 데이터를 또 다시 가져오고 싶진 않을 것 이다.

<br />

### > useEffect

useEffect는 두 개의 `argument`를 가지는 `function`이다.

- 첫번째 argument는 실행시키고 싶은 코드
- 두번째는 dependencies (React.js가 지켜보아야 하는 것들) → 이것들이 변화할 때, 코드를 실행 시킨다.

```jsx
function App() {
  const [counter, setValue] = useState(0);
  const onClick = () => setValue((prev) => prev + 1);
  console.log("i run all the time");

  useEffect(() => {
    console.log("CALL THE API....");
  }, []); // 단 한번만 실행된다.
```

- useEffect function은 코드가 딱 한번만 실행될 수 있도록 보호 해준다.
- 함수 뒤에 [] 빈 array를 써 주었을 때 코드가 단 한번만 실행된다.

```jsx
const [counter, setValue] = useState(0);
const [keyword, setKeyword] = useState("");

useEffect(() => {
  console.log("I run when 'keyword' changes.");
}, [keyword]); // keyword가 update될 때만 코드를 실행
useEffect(() => {
  console.log("I run when 'counter' changes.");
}, [counter]); // counter가 update될 때만 코드를 실행
useEffect(() => {
  console.log("I run when keyword & counter change");
}, [keyword, counter]); // counter와 keyword가 update될 때만 코드를 실행
```

- []에 넣어준 값이 update될 때만 코드를 실행한다.

<br />

### > Cleanup function

component가 없어질 때 어떤 분석 결과를 보내고 싶어한다.

componentrk 사라지거나 없어질 때 event listener를 지우거나 console.log에 무엇인가를 보여줄 수 있다.

```jsx
useEffect(() => {
  console.log("hi");
  return () => console.log("bye");
}, []);
```

- component가 언제 create됐는지, 언제 destroy됐는지 알 수 있다.

<br />

### ✍️ 정리

React.js는 아주 간단한 방법으로 작동 된다.

state를 변화시킬 때 component를 재실행 시키는 것! → 모든 코드를 재실행 시킨다.

이것은 UI 관점으로 보면, 새로운 데이터가 들어올 때마다 자동으로 refresh 되서 좋긴 하지만,

특정 api를 불러오게 되는 경우 계속해서 렌더링이 된다면 성능 저하 문제가 발생할 수도 있기 때문에

**useEffect**를 사용 하여 내가 원하는 부분만을 실행 시킬 수 있다.

💡 참고사항

- 리액트를 사용하는 이유 : 최소 단위의 렌더링을 위해
- `useState()` : 변수와 변수를 제어하는 함수로 구성되며 변하는 값을 제어, 해당 부분의 리렌더링을 위함
- `props` : 태그의 속성 값을 함수의 argument 처럼 컴포넌트에 값을 전달해준다.
- 부모 컴포넌트에서 리렌더링이 일어날 경우 모든 자식 컴포넌트들이 리렌더링 된다. (use memo 👀)
- propType을 설치하고 props의 타입을 지정해 줄 수 있다. 이 때 isRequired로 필수 값을 지정 가능
