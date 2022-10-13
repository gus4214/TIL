# CSS-in-JS (styled-components)

## 1. CSS-in-JS

## > 정의

<aside>
💡 CSS-in-JS는 자바스크립트 파일 안에서 css를 작성할 수 있는 방법

</aside>

현대 웹 애플리케이션은 컴포넌트를 기반으로 발전하기 시작하여 css 스타일링도 컴포넌트를 기반으로 재구성되기 시작하였다.

Sass와 같은 css 전처리기가 등장했음에도 불구하고 자바스크립트의 상태 값을 공유할 수 없어서 동적으로 스타일링을 하기 위해서는 인라인 스타일을 이용하거나 css 클래스 명으로 조건무 스타일링을 이용하는 방식으로 사용하였다.

But! 인라인 스타일을 선언하면 스타일 적용 순위가 높아지며 스타일을 재사용 할 수 없는 문제가 있었고, 클래스이름을 사용했을 때는 css 클래스 증가에 따른 클래스 이름에 대한 고민이 있었다.

이러한 고민 속에 문제를 해결하기 위해 등장한 패러다임이 바로 CSS-in-JS

## > 특징

- js 파일 안에서 css 코드를 작성하기 때문에 css의 변수와 함수를 그대로 사용 가능하다.
- css 클래스명을 해시 값으로 자동으로 생성하여 클래스 이름 작명에 대한 고민의 수고가 덜하다.
- 현대 웹은 컴포넌트 기반으로 발전해 나가기 때문에 컴포넌트와 스타일을 하나의 파일에서 작성하는 CSS-in-JS는 모듈화가 수월해진다.

## > 이용추세

![CSS-in-JS 이용추세 (출저: npm trends)](image/styledcomponents.png)

CSS-in-JS 이용추세 (출저: npm trends)

npm trends에선 최근 5년간 가장 인기 있고 다운로드 되어 사용된 라이브러리가
styled-components이다.

## 2. styled-components

### > 정의

css, Sass에서는 별도의 css, sass 파일을 생성하여 js파일에 import해서 사용했지만, styled-components는 스타일링을 할 때 ES6의 Tagged Templeate Literal 문법을 이용하여 js파일 안에서 선언해서 사용할 수 있다.

**💡 스타일드 컴포넌트의 기본적인 문법**

```jsx
$ npm install styled-components
```

```jsx
// App.js

import React from 'react';
import styled from 'styled-components';          // 1

const App = () => {
  return <Title>styled-components!!</Title>;    // 2
};

const Title = styled.h1`       ⌉
  font-size: 32px;             |
  text-align: center;          |  // 3
  color: purple;               |
`;                             ⌋

export default App;
```

- styled를 import 해준다.
- UI가 그려지는 return문 안에서 <Title></Title> 처럼 컴포넌트를 만들어서 선언 → 선언해준 html 태그가 가지고 있는 속성을 스타일드 컴포넌트로 선언한 컴포넌트에도 적용할 수 있다.
  ```jsx
  <LogoImage src="/images/logo.png" alt="로고" />
  // PascalCase로 컴포넌트 이름 작성
  ```
- styled 객체에 Tagged Templete 문법을 활용해서 css 속성을 정의한다.
  ```jsx
  const [컴포넌트명] = style.[html태그]`
    [부여하고자 하는 css속성]
  `;
  ```
  💡 참고 [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals)

### > 스타일 컴포넌트의 활용

💡 공식문서 : [https://styled-components.com/](https://styled-components.com/)

### **👦 props**

```jsx
// App.js

import React, { useState } from "react";
import styled, { css } from "styled-components";

const App = () => {
  const [changeColor, setChangeColor] = useState(false);

  const handleChanageColor = () => {
    setChangeColor(!changeColor);
  };

  return (
    <>
      <Button onClick={handleChanageColor} primary={changeColor}>
        Button
      </Button>
    </>
  );
};

const Button = styled.button`
  padding: 20px;
  margin: 10px;
  border: none;
  background-color: ${(props) => (props.primary ? "purple" : "pink")}; // 1
`;

export default App;
```

- props로 조건에 따른 스타일링을 동적으로 할 수 있다.

### **👦 상속 스타일**

```jsx
// App.js

const App = () => {
  return (
    <>
      <Button>Button</Button>
      <NewButton>New Button</NewButton>
    </>
  );
};

const Button = styled.button`
  margin: 20px;
  padding: 20px;
  border: none;
  background-color: yellow;
  font-size: 20px;
`;

const NewButton = styled(Button)`
  color: white;
  background-color: purple;
`;

export default App;
```

- 이미 선언된 스타일드 컴포넌트를 활용하여 새로운 스타일드 컴포넌트를 만들 수 있다.
- NewButton 컴포넌트에는 Button 컴포넌트에 적용한 스타일이 그대로 상속되어 추가로 적용한 스타일 이외에는 같은 스타일이 적용된다.

```jsx
// App.js

import { Link } from "react-router-dom";
import styled from "styled-components";

const App = () => {
  return <CartLink to="/cart">장바구니</CartLink>;
};

const CartLink = styled(Link)`
  color: red;
`;

export default App;

// Elements

<a class="sc-eCYdqJ gubPie" href="/cart">
  장바구니
</a>;
```

- 같은 파일에서 선언한 스타일드 컴포넌트뿐만 아니라, Link, 아이콘 라이브러리 등 외부 라이브러리 컴포넌트도 import 하면 위의 예시처럼 스타일을 확장하여 사용 가능하다.

### **👦 네스팅**

아래와 같이 네스팅해서 스타일을 적용할 수 있다.

```jsx
import React from "react";
import styled from "styled-components";

const Main = () => {
  return (
    <List>
      <li>
        메뉴<a href="http://list">클릭</a>
      </li>
    </List>
  );
};

const List = styled.ul`
  padding: 0;

  li {
    padding: 10px 0;
    color: red;
    font-size: 30px;

    a {
      color: green;
    }
  }
`;

export default Main;
```

**But !!** 스타일드 컴포넌트는 **컴포넌트를 분리해서 모듈화하기 위해 최적화** 되어있기 때문에, **네스팅**을 적용해서 사용하는 것보다 **하나의 컴포넌트로 분리**해서 사용하는 것이 더 좋다.

네스팅을 사용해야 하는 경우

```jsx
import React from "react";
import styled from "styled-components";
import Slider from "react-slick";
import "slick-carousel/slick/slick.css";
import "slick-carousel/slick/slick-theme.css";

const Main = () => {
  return <Carousel>// slick 코드</Carousel>;
};

const Carousel = styled(Slider)`
  .slick-slide {
    // slick 커스텀 스타일
  }
`;

export default Main;
```

- react-slick과 같은 외부 라이브러리를 사용하여 이미 정해진 스타일을 변경해야 할 때는 네스팅을 이용해서 스타일링을 해야한다.

### **👦 공통스타일**

### **1. GlobalStyle**

common.css 처럼 전역에 공통으로 css 스타일을 적용해주는 때도 있다.

**createGlobalStyle** 함수를 통해 **전역에 적용**하기 위한 스타일 컴포넌트를 생성할 수 있다.

```jsx
// src/styles/GlobalStyle.js

import React from "react";
import { createGlobalStyle } from "styled-components";

const GlobalStyle = createGlobalStyle`
  * {
    box-sizing: border-box;
    font-family: 'Noto Sans KR', sans-serif;
  }
`;

export default GlobalStyle;
```

👇

```jsx
// index.js

import React from "react";
import ReactDOM from "react-dom/client";
import { ThemeProvider } from "styled-components";
import Router from "./Router";
import GlobalStyle from "./styles/GlobalStyle";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <ThemeProvider>
    <GlobalStyle />
    <Router />
  </ThemeProvider>
);
```

- createGlobalStyle 함수로 생성한 GlobalSyle 컴포넌트를 전역스타일에 적용해주고 싶은 컴포넌트 상위에 적용해주면 하위 컴포넌트에 적용된다.

### **2. styled-reset**

reset.css 처럼 기본 스타일을 초기화 해주는 작업을 GlobalStyle.js 파일에 선언하여 전역에 적용할 수 있다.

1. 설치

   ```jsx
   $ npm install styled-reset
   ```

2. 선언방법 (createGlobalStyle``; 안에 ${reset}을 선언해준다.)

   ```jsx
   // src/styles/GlobalStyle.js

   import React from "react";
   import { createGlobalStyle } from "styled-components";
   import reset from "styled-reset";

   const GlobalStyle = createGlobalStyle`
     ${reset}
   
     * {
       box-sizing: border-box;
       font-family: 'Do Hyeon', sans-serif;
     }
   `;

   export default GlobalStyle;
   ```

### **3. ThemeProvider**

sass에서는 변수와 mixin 등 공통으로 사용할 스타일에 대해서 파일을 만들고, 사용 하고자 하는 scss 파일에 import를 해서 적용 시켰다. 하지만 매번 import를 해주고, 참조해야 하는 css 파일이 많아지면 의존성을 관리하기도 힘들어진다.

→ 이런 문제를 해결하기 위해서 스타일 컴포넌트에서는 ThemeProvider를 통해 전역으로 테마, JS변수 등을 공유하여 사용한다.

```jsx
// index.js

import React from "react";
import ReactDOM from "react-dom/client";
import { ThemeProvider } from "styled-components";
import GlobalStyle from "./styles/GlobalStyle";
import theme from "./styles/theme";
import Router from "./Router";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <ThemeProvider theme={theme}>
    <GlobalStyle />
    <Router />
  </ThemeProvider>
);
```

- ThemeProvider는 위의 예시와 같이 프로젝트의 엔트리 포인트인 index.js의 최초로 렌더링 되는 컴포넌트를 감싸주어서 모든 컴포넌트의 prop에 theme을 부여하여 적용할 수 있다.

**1. theme**

```jsx
// theme.js

const theme = {
  black: "#000000",
  white: "#FFFFFF",
  lightGrey: "#B0B0B0",
  middleGrey: "#717171",
  deepGrey: "#222222",
  hoverGrey: "#DBDBDB",
};

export default theme;
```

- color, fontSize등 공통된 테마는 theme.js에서 선언하여 각 컴포넌트에서 props로 받아 스타일을 적용할 수 있다.
- ThemeProvider의 속성으로 넘겨주면 전역에서 사용가능

```jsx
// App.js

import { Link } from "react-router-dom";
import styled from "styled-components";

const App = () => {
  return <Container>title</Container>;
};

const Container = styled.div`
  background-color: ${(props) => props.theme.lightGrey};
`;
```

```jsx
// App.js

const Container = styled.div`
  background-color: ${props => console.log(props)}
`;

// console.log(props)의 결과

props: {
    children: 'title',
    theme: {
      black: '#000000',
      white: '#FFFFFF',
      lightGrey: '#B0B0B0',
      middleGrey: '#717171',
      deepGrey: '#222222',
      hoverGrey: '#DBDBDB',
    },
  },
```

- 전역적으로 사용하기 위한 theme.js 파일을 만들고, 해당 파일을 index.js에서 ThemeProvider를 통해 설정해 주면, 위의 예시처럼 props로 받아와서 사용할 수 있다.
- 어떤 형태로 들어오는지 console.log 로 확인을 해보면 props는 다음과 같은 객체 형태로 데이터가 들어오게 된다. 그래서 props.theme.ligthrgrey로 값을 사용할 수가 있게 된다 👍

**2. mixin**

자주 사용하는 css 스타일에 대해서는 variables.js 파일을 별도로 생성하여 사용하는 것이 좋다.

variables.js 파일은 theme과 variables를 Theme Provider에 같이 prop으로 합쳐서 전역에서 사용하거나, 사용하고자 하는 파일에서만 import해서 mixin을 사용할 수 있다.

```jsx
// variables.js

import { css } from "styled-components";

const variables = {
  flex: (direction = "row", justify = "center", align = "center") => `
    display: flex;
    flex-direction: ${direction};
    justify-content: ${justify};
    align-items: ${align};
  `,

  absoluteCenter: css`
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  `,
};

export default variables;
```

- **ThemeProvider에서 prop으로 합쳐서 사용**

  ```jsx
  // index.js

  import React from "react";
  import ReactDOM from "react-dom/client";
  import { ThemeProvider } from "styled-components";
  import GlobalStyle from "./styles/GlobalStyle";
  import theme from "./styles/theme";
  import variables from "./styles/variables";
  import Router from "./Router";

  const root = ReactDOM.createRoot(document.getElementById("root"));
  root.render(
    <ThemeProvider theme={{ style: theme, variables }}>
      <GlobalStyle />
      <Router />
    </ThemeProvider>
  );
  ```

  사용할 때는 다음과 같이 적용!

  ```jsx
  // App.js

  const App = () => {
    return (
      <Container>
        <Button>첫번째 버튼</Button>
        <Button>두번째 버튼</Button>
      </Container>
    );
  };

  const Container = styled.div`
    ${(props) => props.theme.variables.flexSet()}
  `; // a

  const Button = styled.button`
    background-color: ${(props) => props.theme.style.lightGrey};
  `;

  export default App;
  ```

  variables.js 파일에서 기본으로 설정한 값을 사용할 때는 flexSet()을 써주고, 다른 인자를 넘겨줄때는 `${(props) => props.theme.variables.flexSet(’’,’space-between’,’center’)}` 처럼 적용하고 싶은 인자를 넘겨줄 수 있다.

- **각 컴포넌트에서 variables.js 파일을 import해서 사용**

  ```jsx
  // App.js

  import styled from "styled-components";
  import variables from "./styles/variables";

  const App = () => {
    return (
      <Wrapper>
        <Button primary="pink">Pink Button</Button>
        <Button primary="Yellow">Yellow Button</Button>
      </Wrapper>
    );
  };

  const Wrapper = styled.div`
    ${variables.flex()}
  `;

  const Button = styled.button`
    margin: 20px;
    padding: 20px;
    border: none;
    background-color: ${(props) => props.primary};
    font-size: 20px;
  `;

  export default App;
  ```

### 4. 글로벌 폰트

전역에서 사용하길 원하면 GlobalStyle.js의 body안에 font-family를 웹 폰트 명으로 지정해주어야 한다.

웹 폰트를 사용할 것인지, 폰트 파일을 사용할 것인지에 대해서 설정방법이 달라진다.

```jsx
// GlobalStyle.js

import { createGlobalStyle } from "styled-components";
import reset from "styled-reset";

const GlobalStyle = createGlobalStyle`
  ${reset}
  
  body{
    font-family: 'Do Hyeon', sans-serif;
  }

`;

export default GlobalStyle;
```

1. **웹 폰트**

   ```jsx
   // index.html

   <head>
     <link rel="preconnect" href="https://fonts.googleapis.com" />
     <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
     <link
       href="https://fonts.googleapis.com/css2?family=Do+Hyeon&display=swap"
       rel="stylesheet"
     />
   </head>
   ```

   - 웹 폰트 사용할 때는 웹 폰트 사이트에서 제공하는 embedding(임베드) 코드를 복사하여 html 파일에 코드를 추가해야 한다.
   - index.html의 head안에 link 태그를 이용해서 글로벌 폰트로 지정해서 사용할 수 있다.

2. **폰트파일**

   ```jsx
   src
   └── styles
       ├── fonts
       │   └── DoHyeon-Regular.ttf
       ├── GlobalFont.js
       ├── GlobalStyle.js
       └── theme.js
   ```

   - styles 폴더 안에 폰트파일을 저장할 폴더를 생성하여 폰트파일을 넣어준다.

   ```jsx
   // src/styles/GlobalFont.js

   import { createGlobalStyle } from "styled-components";
   import DoHyeon from "./fonts/DoHyeon-Regular.ttf";

   const GlobalFont = createGlobalStyle`
   	@font-face { 
       font-family: 'Do Hyeon';
       src: url(${DoHyeon}) format('woff');
     }
   `;

   export default GlobalFont;
   ```

   - 스타일드 컴포넌트의 createGlobalStyle을 통해 글로벌 스타일을 생성해준다. 이 때 @font-face를 사용하여 웹 페이지에 적용 가능

   ```jsx
   // index.js

   import React from "react";
   import ReactDOM from "react-dom/client";
   import { ThemeProvider } from "styled-components";
   import GlobalStyle from "./styles/GlobalStyle";
   import GlobalFont from "./styles/GlobalFont";
   import color from "./styles/theme";
   import Router from "./Router";

   const root = ReactDOM.createRoot(document.getElementById("root"));
   root.render(
     <ThemeProvider theme={theme}>
       <GlobalStyle />
       <GlobalFont />
       <Router />
     </ThemeProvider>
   );
   ```

   - 전역에서 사용하기 위해서는 위와 같이 적용해서 사용!
