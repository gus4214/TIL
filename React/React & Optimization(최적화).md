# React & Optimization(최적화)

<br />

# react.memo()로 불필요한 재평가 방지

```jsx
function App() {
  const [show, setShow] = useState(false);

  console.log("APP RUNNING");

  const onToggle = () => {
    setShow((prevShow) => !prevShow);
  };

  return (
    <div className="app">
      <h1>Hi there!</h1>
      <DemoOutput show={false} />
      <Button onClick={onToggle}>Toggle Paragraph!</Button>
    </div>
  );
}
```

```jsx
const Button = (props) => {
  console.log("Button RUNNING");
  return (
    <button type={props.type || "button"} onClick={props.onClick}>
      {props.children}
    </button>
  );
};

export default Button;
```

```jsx
const DemoOutput = (props) => {
  console.log("DemoOutput RUNNING");
  return <Paragraph>{props.show ? "new" : ""}</Paragraph>;
};

export default React.memo(DemoOutput);
```

```jsx
const Paragraph = (props) => {
  console.log("Paragraph RUNNING");
  return <p>{props.children}</p>;
};

export default Paragraph;
```

`React.memo`는 함수형 컴포넌트를 **최적화**할 수 있다.

위의 코드에서 memo는 인자로 들어간 `DemoOutput` 컴포넌트에 어떤 props가
입력되는지 확인하고 입력되는 모든 props의 신규 값을 확인한 뒤 이른 기존의 props의 값과 비교하도록 리액트에게 전달한다.

⇒ 그리고 props의 값이 바뀐 경우에만 컴포넌트를 재실행 및 재평가하게 된다.

⇒ 부모 컴포넌트가 변경되었지만 그 컴포넌트의 props 값이 바뀌지 않았다면 컴포넌트 실행은 건너뛴다.

- 처음에는 App이 처음으로 렌더링되기 때문에 `DemoOutput` 은 바로 실행
- 하지만, 콘솔을 초기화한 뒤 버튼을 누르면 콘솔에는 ‘APP RUNNING’ 과
  ’Button RUNNING’ 만 확인되고 ‘DemoOutput RUNNING’은 출력되지 않는다.
- ‘Paragraph RUNNING’ 또한 자식관계이기 때문에 재실행 되지 않아 출력되지 않는다.

이렇게 memo는 불필요한 재렌더링을 피하기 위해 최적화가 이루어진다.

<br />

### 그렇다면 왜 모든 컴포넌트에 memo를 적용하지 않는걸까??

<br />

최적화에는 비용이 따른다.

memo 메소드는 App에 변경이 발생할 때마다 이 컴포넌트로 이동하여
기존 props 값과 새로운 값을 비교하게 한다.

그러면 리액트는 기존의 props 값을 저장할 공간이 필요하고 비교하는 작업도 필요하여 두가지 작업을 할 수 있어야 한다.

이 각각의 작업은 개별적인 성능 비용이 필요하고, 성능 효율은 어떤 컴포넌트를 최적화 하느냐에 따라 달라지게 된다.

컴포넌트를 재평가하는데 필요한 성능 비용과 props를 비교하는 성능 비용을 서로 맞바꾸는 것!

→ **props의 개수와 컴포넌트의 복잡도, 자식 컴포넌트의 숫자에 따라 달라지므로 어느 쪽의 비용이 더 높다고 말하는 것은 불가능하다.**

물론 자식 컴포넌트가 많아서 컴포넌트 트리가 매우 크다면 memo는 유용하게 쓰일 수 있다.

그리고 컴포넌트 트리의 상위에 위치해있다면 전체 컴포넌트 트리에 대한 쓸데없는 재렌더링을 막을 수 있다.

위의 `DemoOutput` 의 재평가를 피함으로 자동적으로 `Paragrapg` 의 재평가 역시 피할 수 있었다.

컴포넌트 트리 전체의 가지를 잘라냈기 때문 → 이것이 `React.memo`가 유용한 분야

하지만 반대로 부모 컴포넌트를 매번 재평가할 때마다 컴포넌트의 변화가 있거나 props의 값이 변화하는 경우라면 `React.memo` 는 크게 의미를 갖지 못한다.

(컴포넌트의 재렌더링이 어떻게든 필요하기 때문)

앱 크기에 따라서도 달라지는데, 매우 작은 앱이나 작은 컴포넌트 트리의 경우에는 이런 과정을 추가하는 것이 필요가 없을 수 있다.
**하지만 불필요한 재평가를 cut할 수 있는 큰 규모의 앱이라면 가치가 있겠지!!!**

모든 컴포넌트를 memo로 래핑할 필요는 없고 컴포넌트 트리에서 잘라낼 수 있는 몇 가지의 주요 컴포넌트 부분을 선택해서 사용하면 된다.

<br />

### 위의 코드에서 버튼의 경우 memo를 적용할 것인지??

<br />

우리는 개발자로서 이 `<Button />` 이 다시 변경될 일이 없다는 것을 안다.

그러므로 **버튼에 대해 매번 재평가하는 것은 가치가 없다.**

(같은 텍스트, 같은 함수를 사용하니)

그렇다면 버튼 컴포넌트를 **React.memo**를 이용하여 래핑해보자

```jsx
function App() {
  const [show, setShow] = useState(false);

  console.log("APP RUNNING");

  const onToggle = () => {
    setShow((prevShow) => !prevShow);
  };

  return (
    <div className="app">
      <h1>Hi there!</h1>
      <DemoOutput show={false} />
      <Button onClick={onToggle}>Toggle Paragraph!</Button>
    </div>
  );
}
```

```jsx
const Button = (props) => {
  console.log("Button RUNNING");
  return (
    <button type={props.type || "button"} onClick={props.onClick}>
      {props.children}
    </button>
  );
};

export default React.memo(Button);
```

여기서 App을 새로고침하면 콘솔에 ‘Button RUNNING’이 표시된다.

다시 표시가 된다는 것은 props의 값이 계속 바뀐다는 뜻인데 ?!!!

props로 받은것은 `onClick` 이라는 props와 ‘Toggle Paragraph!'이라는 텍스트자식까지 총 2개인데, 이 둘의 값은 변하지 않는 값이다. 텍스트도 같고 실행되는 함수도 항상 같다.

👉 **이것은 리액트에서 흔하게 발생하는 오류 중에 하나!**

App 컴포넌트는 어찌됐건 함수이기 때문에 마치 일반적인 자바스크립트 함수처럼 재실행된다.

왜냐하면, 결국 이 것은 상태가 바뀌게 되면 일반적인 자바스크립트 함수와 같으니깐!

여기서 조금 다른것은

**이 App 함수는 사용자가 아닌 리액트에 의해 호출된다는 것이다.**

이 말은 App 함수안 모든 코드가 다시 실행된다는 의미!! 이것은 중요한 의미가 있다.

물론 버튼에 전달되는 `onToggle` 함수는 매번 재생성된다.

이는 App 함수의 모든 렌더링, 또는 모든 실행 사이클에서 완전히 **새로운 함수**라는것

재사용하지 않는다 → **우리가 매번 다시 만드는 상수**이기 때문

App함수 안에 있는 모든 코드가 다시 실행되므로 당연히, `onToggle` 도 새로운 함수가 만들어진다.
이 것은 이전과 같은 함수가 아니고 같은 기능을 하는 새로운 함수

→ **자바스크립트에서 App 함수가 실행될 때마다 만들어지는 함수는 모두 새로운 함수이다.**

앞에서 `DemoOutput` 은 memo로 래핑했기 때문에 절대 변하지 않는다고 했었다.

```jsx
const DemoOutput = (props) => {
  console.log("DemoOutput RUNNING");
  return <Paragraph>{props.show ? "new" : ""}</Paragraph>;
};

export default React.memo(DemoOutput);
```

그럼 App 함수가 재실행된다고 했으니 매번 props로 받은 `false` 값이 새로 만들어지는 것인데 마지막 렌더링 사이클에서 false가 발생했더라도 재실행되면 새로운 `false` 가 생성되는 것

<br />

🤔 **그럼 이 경우에서 React.memo가 `DemoOutput` 에서는 작동하는데 왜 버튼에서는 작동하지 않는 것일까 ???**

`false` 와 `onToggle` 은 뭐가 다르길래?!

false는 boolean 값으로 문자열, 또는 숫자와 같은 **자바스크립트의 원시 값**이다.

React.memo가 최종적으로 하는 일은 props 값을 확인하고 props.show를

그 직전의 값인 props.previous.show와 비교하는 것

(props.show === props.previous.show) ← 이런식으로

이 작업은 일반 비교 연산자를 통해 하는데

**원시값이라면 true가 나오지만 배열이나 객체, 함수를 비교한다면 말이 달라진다.**

자바스크립트에서 함수는 하나의 객체에 불과하다.

리액트가 아닌 자바스크립트이기 때문에 App 함수가 실행될 때마다 새로운 함수 객체가 생성되고 이 함수 객체가 props로 전달된다.

(props.onClick === props.previous.onClick)

이 경우에 두 함수 객체는 같은 내용을 갖고 있다 해도 자바스크립트에서 이 둘을 비교하면 동일하지 않다.
⇒ **원시값과 참조값의 차이!!**

React.memo는 이러한 자바스크립트의 작동방식 때문에 값이 변경되었다고 인식하게 되는 것이다.

**이 것은 일반적인 이슈 중 하나로 많은 개발자들이 어려움을 겪고 있다고 함!!!**

그렇다면 React.memo는 props를 통한 객체나 배열, 함수를 가져오는 컴포넌트에는 사용할 수 없는 것인가???

아니쥐~!~!~! 다른 해결책이 있다.

<br />

# useCallback()

## useCallback()으로 함수 재생성 방지

React.memo는 객체 외 prop 값에도 작동하게끔 할 수 있다.

리액트에서 제공하는 훅인 useCallback훅을 사용하면 된다.

> useCallback
> 컴포넌트 실행 전반에 걸쳐 함수를 저장할 수 있게 하는 훅

예를 들어

```jsx
let obj1 = {};
let obj2 = {};
obj1 === obj2; // false

obj2 = obj1;
obj1 === obj2; // true
```

이 것이 `useCallback` 이 하는 일로 우리가 선택한 함수를 리액트의 내부 저장 공간에 저장을 해서 함수 객체가 실행될 때마다 이를 재사용할 수 있게 된다.

사용법은 저장하려는 함수를 래핑하면 된다.

```jsx
import { useCallback, useState } from "react";

function App() {
  const [show, setShow] = useState(false);

  console.log("APP RUNNING");

  const onToggle = useCallback(() => {
    setShow((prevShow) => !prevShow);
  }, []);

  return (
    <div className="app">
      <h1>Hi there!</h1>
      <DemoOutput show={false} />
      <Button onClick={onToggle}>Toggle Paragraph!</Button>
    </div>
  );
}
```

어떤 함수가 절대 변경되어선 안된다면 `useCallback` 을 사용해 함수를 저장하면 된다.

useCallback도 useEffect와 같이 두번째 인자에 의존성 배열을 추가할 수 있다.

onToggle함수는 내용이 없는 의존성 배열이 있는데, 이는 onToggle에 저장하려고 하는 이 콜백 함수는 절대 변경되지 않을 거싱라고 리액트에 알려주는 배열 []

따라서 App 컴포넌트가 다시 렌더링돼도 항상 같은 함수 객체가 사용되게끔 한다.

```jsx
const Button = (props) => {
  console.log("Button RUNNING");
  return (
    <button type={props.type || "button"} onClick={props.onClick}>
      {props.children}
    </button>
  );
};

export default React.memo(Button);
```

이렇게 전달한 모든 props 값이 비교가 가능하게끔 전달했기 때문에 memo의 역할을 수행할 수 있다.

**onToggle 객체가 useCallback 덕분에 메모리 안에서 항상 같은 객체임을 보증하기 때문!!**

<br />

## useCallback() 및 해당 종속성

```jsx
const onToggle = useCallback(() => {
  setShow((prevShow) => !prevShow);
}, []);
```

이제 의존성 배열을 지정해야 하는데

위의 함수는 모든 재렌더링 주기마다 항상 똑같은 로직을 쓰는데 왜 필요한건지?!

👦 **자바스크립트에서 함수는 클로저**

즉, 이 환경에서 사용할 수 있는 값에 클로저를 만들게 된다.

리액트의 작동방식을 이해하려면 클로저가 무엇인지를 알아야한다.

예시)

```jsx
function App() {
  const [show, setShow] = useState(false);
  const [allowToggle, setAllowToggle] = useState(false);

  console.log("APP RUNNING");

  const onToggle = useCallback(() => {
    if (allowToggle) {
      setShow((prevShow) => !prevShow);
    }
  }, []);

  const allowToggling = () => {
    setAllowToggle(true);
  };

  return (
    <div className="app">
      <h1>Hi there!</h1>
      <DemoOutput show={show} />
      <Button onClick={allowToggling}>Allow Toggle</Button>
      <Button onClick={onToggle}>Toggle Paragraph!</Button>
    </div>
  );
}
```

위와 같이 Allow Toggle를 할 수 있게 해주는 버튼을 하나 추가한뒤

`allowToggling` 이라는 함수를 만들었다.

여기서 allowToggle의 상태 스냅샷을 활용하여 setShow를 사용할 수 있는지 확인해보자

allowToggle이 true일 경우에만 setShow를 호출한다.

이렇게 되면 show의 상태는 토글이 허용되는 경우에만 업데이트 됨

자바스크립트의 함수는 클로저이다 이 말은,

App 함수에 있는 onToggle 블록 안의 함수
`if(allowToggle){setShow((prevShow) => !prevShow);};`가 정의될 때

**자바스크립트는 이 안에서 사용되는 모든 변수를 잠그게 된다.**

**→ 함수 외부에서 사용하는 모든 변수**

여기서는 if문 안의 allowToggle이 해당하는데, 이 것은 App 함수 외부에 있는 변수나 상수이고 이 allowToggle을 함수 안에서 사용하고 있다.

따라서, 자바스크립트는 이 상수(allowToggle)에 클로저를 만들고 함수를 정의할 때 사용하기 위해 상수를 저장한다.

이렇게 되면 다음에 onToggle이 실행이 되면 if문 안에 있는 allowToggle 상수를 그대로 사용하게 된다.

```jsx
if (allowToggle) {
  setShow((prevShow) => !prevShow);
}
```

따라서 allowToggle 변수의 값은 변수가 저장된 시점의 값을 사용하게 되는 것

이제 문제는 useCallback을 사용하여 리액트에게 해당 함수(onToggle)를 저장하라고 지시할 수 있다. 그러면 이 함수는 메모리 어딘가에 저장이 된다.

```jsx
const onToggle = useCallback(() => {
  if (allowToggle) {
    setShow((prevShow) => !prevShow);
  }
}, []);

const allowToggling = () => {
  setAllowToggle(true);
};
```

App 함수가 토글 상태가 true로 변경되어 재평가, 재실행된다면 리액트는 onToggle안에 있는 함수를 재생성하지 않는다.

왜냐하면 useCallback을 통해 리액트에게 어떤 환경에서든 함수 재생성을 하지 않게 막았으니깐!

**따라서 이 함수에 사용하기 위해 저장한 allowToggle의 값은 최신의 값이 아닌 App 컴포넌트가 처음 실행된 시점의 값을 저장하고 있다.**

당연히 이러한 것은 함수 재생성을 필요로 하는 때가 있을 수 있으므로 문제가 된다.

```jsx
const onToggle = useCallback(() => {
  if (allowToggle) {
    setShow((prevShow) => !prevShow);
  }
}, [allowToggle]);
```

의존성 배열에 allowToggle을 종속 형태로 추가한다.

allowToggle의 값이 바뀌고 새로운 값이 들어오면, 함수를 재생성하고 이 새로 만든 함수를 저장하길 원한다.

이렇게 하면 함수에 항상 allowToggle의 최신 값만을 사용하게 되는 것

allowToggle이 변경되지 않는다면 함수 재생성을 하지 않고!!

<aside>
💡 이렇게 클로저가 어떻게 작동하는 지를 이해하고 원시값과 참조값에 대한 이해가 충분하면 리액트의 작동 원리를 완벽하게 이해할 수 있다!!

</aside>

<br />

# 정리

리액트 앱에서는 컴포넌트를 통해 작업을 수행

이러한 컴포넌트는 결국 하나의 작업을 수행하는데 이들이 반환하는 JSX 코드이다.

이 것은 리액트에게 컴포넌트의 출력이 무엇인지를 알려준다.

→ 상태와 props, 컨텍스트를 이용해 작업할 수 있고 props와 컨텍스트는 결국 상태의 변경으로 이어지기 때문에 컴포넌트의 변경과 컴포넌트에 영향을 주는,

또는 어플리케이션 일부에 영향을 미치는 데이터를 변경하게 된다.

컴포넌트에서 상태를 변경할 때마다 이 변경된 상태가 있는 컴포넌트는 재평가된다.

👉 컴포넌트 함수가 재실행된다는 의미

따라서 모든 코드가 재실행되고 새로운 출력값을 얻을 수 있다.

리액트는 단순히 최신 평가의 결과를 가져와서 직전 평가의 결과와 비교한다.

이는 모든 컴포넌트에 해당

그리고 확인된 모든 변경 사항이나 차이점을 리액트 DOM에 전달한다.

(리액트 DOM을 통해 index.js 파일을 렌더링하기 때문)

리액트 DOM은 이 변경 사항을 브라우저의 실제 DOM에 적용하고 변경되지 않는 것들은 그대로 둔다.

이제 리액트가 컴포넌트를 재평가할 때 단순히 컴포넌트 재평가에서 그치지 않고 전체 함수를 재실행하고 이를 통해 코드를 전부 리빌드한다.

JSX 코드가 최신 스냡샷의 출력 결과를 리빌드하는 것

그리고 JSX 코드에 있는 모든 컴포넌트를 재실행한다.
