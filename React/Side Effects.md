# Side Effects

사이드이펙트는 과연 무엇일까??

리액트 라이브러리 자체는 UI를 렌더링하는 주요 임무가 있다.

사용자 입력에 반응하여 필요할 때 UI를 다시 렌더링 하는 것!!

state나 event 그 모든 것의 임무는 화면에 무언가를 겨져오는 것이었지

→ 사용자가 그 무언가와 상호 작용하게 하는 것

그리고 화면에 보이는 것은 특정 이벤트에 따라 변경될 수 있다.

ex) 버튼이 클릭되거나 텍스트가 입력되는 것에 따라서

👉 즉, 이것이 리액트가 애플리케이션에서 주로 하는 일이다.

<br />

리액트 컴포넌트를 살펴보자

컴포넌트는 단지 함수이며 위에서 아래로 실행된다.

그리고 함수 안에 있는 모든 것은 결국 화면에 무언가를 가져 오는 것에 관한 것이다.

(클릭 등의 사용자 입력에 반응함으로써)

state를 사용할 수도 있고 다른 함수가 있을 수도 있다.

ex) 버튼을 눌렀을 때 트리거되는 함수 같은 것

![리액트의 주요 임무](/React/Image/sideEffects1.png)

리액트의 주요 임무

<br />

**따라서 사이드이펙트는 애플리케이션에서 일어나는 다른 모든 것을 뜻한다.**

예를들면)

http 리퀘스트를 보내는 것, 또는 브라우저 저장소에 무언가를 저장하는 것, 코드에서 타이머나 간격을 설정할 수도 있다.

이것들은 모두 애플리케이션에서 고려해야 하는 작업이다.

예를 들어, 웹 애플리케이션은 대부분 백엔드 서버에 http 리퀘스트를 보내야 한다.

하지만 이러한 작업들은 화면에 무언가를 가져오는 것과는 직접적인 관련이 없다.

🤔 리퀘스트를 보내는 것 자체나 잠재적 오류를 처리하는 것 등은 리액트를 필요로 하지 않는다.

- 그것은 리액트가 신경쓰는 것이 아니며
- 그런 일을 하려고 리액트가 있는 게 아니다
- 화면에 직접 무언가를 그리는 작업이나 그외 비슷한 작업들과 관련되어 있지 않다.

👉 따라서 이것들은 일반적인 컴포넌트 평가의 밖에서 일어나야 하는 일이다.

(즉, 일반적인 컴포넌트 함수 밖에서)

![스크린샷 2022-11-18 오후 5.30.27.png](/React/Image/sideEffects2.png)

```jsx
function App(){
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  const loginHandler = (email, password) => {
     setIsLoggedIn(true);
  };

  const logoutHandler = () => {
     setIsLoggedIn(false);
  };

  return (
    <>
      <MainHeader isAuthenticated={isLoggedIn} onLogout={logoutHandler} />
      <main>
        {!isLoggedIn && <Login onLogin={loginHandler} />}
        {isLoggedIn && <Home onLogout={logoutHandler} />}
      </main>
    <>
  );
}

export default App;
```

예를 들어 위의 `App()` 함수는 컴포넌트 함수의 state가 변경될 때마다 리액트에 의해 자동으로 재실행 될 것이다.

그러면 리액트는 기본적으로

```jsx
  return (
    <>
      <MainHeader isAuthenticated={isLoggedIn} onLogout={logoutHandler} />
      <main>
        {!isLoggedIn && <Login onLogin={loginHandler} />}
        {isLoggedIn && <Home onLogout={logoutHandler} />}
      </main>
    <>
  );
```

이 함수를 새로 실행한 결과를 확인하고 새 JSX 코드가 어떻게 보이는지 확인한다.

이전 결과와 비교하고 실제 DOM으로 이동하여 거기에서 약간의 변경을 한다.

→ 이것이 리액트가 하는 일

여기서 예를 들어 http 리퀘스트를 직접 App 함수에 보내면 다시 실행될 때마다 리퀘스트를 다시 보내게 될 것이다.

그렇게 하는 것이 필요할 때도 있지만 항상 그런건 아니겠지

http 리퀘스트에 대한 응답으로 어떤 state를 변경한다면 무한 루프로도 빠질 수 있다.

따라서 이런 사이드이펙트는 직접적으로 이 컴포넌트 함수에 들어가서는 안된다.

→ 버그나 무한 루프가 발생할 가능성이 높기 때문에

그러므로 사이드이펙트를 처리하는 더 좋은 도구가 필요하다!!

👉 **useEffect 훅을 사용할 것**

---
