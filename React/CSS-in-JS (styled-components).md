# CSS-in-JS (styled-components)

## 1. CSS-in-JS

## > ์ ์

<aside>
๐ก CSS-in-JS๋ ์๋ฐ์คํฌ๋ฆฝํธ ํ์ผ ์์์ css๋ฅผ ์์ฑํ  ์ ์๋ ๋ฐฉ๋ฒ

</aside>

ํ๋ ์น ์ ํ๋ฆฌ์ผ์ด์์ ์ปดํฌ๋ํธ๋ฅผ ๊ธฐ๋ฐ์ผ๋ก ๋ฐ์ ํ๊ธฐ ์์ํ์ฌ css ์คํ์ผ๋ง๋ ์ปดํฌ๋ํธ๋ฅผ ๊ธฐ๋ฐ์ผ๋ก ์ฌ๊ตฌ์ฑ๋๊ธฐ ์์ํ์๋ค.

Sass์ ๊ฐ์ css ์ ์ฒ๋ฆฌ๊ธฐ๊ฐ ๋ฑ์ฅํ์์๋ ๋ถ๊ตฌํ๊ณ  ์๋ฐ์คํฌ๋ฆฝํธ์ ์ํ ๊ฐ์ ๊ณต์ ํ  ์ ์์ด์ ๋์ ์ผ๋ก ์คํ์ผ๋ง์ ํ๊ธฐ ์ํด์๋ ์ธ๋ผ์ธ ์คํ์ผ์ ์ด์ฉํ๊ฑฐ๋ css ํด๋์ค ๋ช์ผ๋ก ์กฐ๊ฑด๋ฌด ์คํ์ผ๋ง์ ์ด์ฉํ๋ ๋ฐฉ์์ผ๋ก ์ฌ์ฉํ์๋ค.

But! ์ธ๋ผ์ธ ์คํ์ผ์ ์ ์ธํ๋ฉด ์คํ์ผ ์ ์ฉ ์์๊ฐ ๋์์ง๋ฉฐ ์คํ์ผ์ ์ฌ์ฌ์ฉ ํ  ์ ์๋ ๋ฌธ์ ๊ฐ ์์๊ณ , ํด๋์ค์ด๋ฆ์ ์ฌ์ฉํ์ ๋๋ css ํด๋์ค ์ฆ๊ฐ์ ๋ฐ๋ฅธ ํด๋์ค ์ด๋ฆ์ ๋ํ ๊ณ ๋ฏผ์ด ์์๋ค.

์ด๋ฌํ ๊ณ ๋ฏผ ์์ ๋ฌธ์ ๋ฅผ ํด๊ฒฐํ๊ธฐ ์ํด ๋ฑ์ฅํ ํจ๋ฌ๋ค์์ด ๋ฐ๋ก CSS-in-JS

## > ํน์ง

- js ํ์ผ ์์์ css ์ฝ๋๋ฅผ ์์ฑํ๊ธฐ ๋๋ฌธ์ css์ ๋ณ์์ ํจ์๋ฅผ ๊ทธ๋๋ก ์ฌ์ฉ ๊ฐ๋ฅํ๋ค.
- css ํด๋์ค๋ช์ ํด์ ๊ฐ์ผ๋ก ์๋์ผ๋ก ์์ฑํ์ฌ ํด๋์ค ์ด๋ฆ ์๋ช์ ๋ํ ๊ณ ๋ฏผ์ ์๊ณ ๊ฐ ๋ํ๋ค.
- ํ๋ ์น์ ์ปดํฌ๋ํธ ๊ธฐ๋ฐ์ผ๋ก ๋ฐ์ ํด ๋๊ฐ๊ธฐ ๋๋ฌธ์ ์ปดํฌ๋ํธ์ ์คํ์ผ์ ํ๋์ ํ์ผ์์ ์์ฑํ๋ CSS-in-JS๋ ๋ชจ๋ํ๊ฐ ์์ํด์ง๋ค.

## > ์ด์ฉ์ถ์ธ

![CSS-in-JS ์ด์ฉ์ถ์ธ (์ถ์ : npm trends)](image/styledcomponents.png)

CSS-in-JS ์ด์ฉ์ถ์ธ (์ถ์ : npm trends)

npm trends์์  ์ต๊ทผ 5๋๊ฐ ๊ฐ์ฅ ์ธ๊ธฐ ์๊ณ  ๋ค์ด๋ก๋ ๋์ด ์ฌ์ฉ๋ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๊ฐ
styled-components์ด๋ค.

## 2. styled-components

### > ์ ์

css, Sass์์๋ ๋ณ๋์ css, sass ํ์ผ์ ์์ฑํ์ฌ jsํ์ผ์ importํด์ ์ฌ์ฉํ์ง๋ง, styled-components๋ ์คํ์ผ๋ง์ ํ  ๋ ES6์ Tagged Templeate Literal ๋ฌธ๋ฒ์ ์ด์ฉํ์ฌ jsํ์ผ ์์์ ์ ์ธํด์ ์ฌ์ฉํ  ์ ์๋ค.

**๐กย ์คํ์ผ๋ ์ปดํฌ๋ํธ์ ๊ธฐ๋ณธ์ ์ธ ๋ฌธ๋ฒ**

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

const Title = styled.h1`       โ
  font-size: 32px;             |
  text-align: center;          |  // 3
  color: purple;               |
`;                             โ

export default App;
```

- styled๋ฅผ import ํด์ค๋ค.
- UI๊ฐ ๊ทธ๋ ค์ง๋ return๋ฌธ ์์์ <Title></Title> ์ฒ๋ผ ์ปดํฌ๋ํธ๋ฅผ ๋ง๋ค์ด์ ์ ์ธ โ ์ ์ธํด์ค html ํ๊ทธ๊ฐ ๊ฐ์ง๊ณ  ์๋ ์์ฑ์ ์คํ์ผ๋ ์ปดํฌ๋ํธ๋ก ์ ์ธํ ์ปดํฌ๋ํธ์๋ ์ ์ฉํ  ์ ์๋ค.
  ```jsx
  <LogoImage src="/images/logo.png" alt="๋ก๊ณ " />
  // PascalCase๋ก ์ปดํฌ๋ํธ ์ด๋ฆ ์์ฑ
  ```
- styled ๊ฐ์ฒด์ Tagged Templete ๋ฌธ๋ฒ์ ํ์ฉํด์ css ์์ฑ์ ์ ์ํ๋ค.
  ```jsx
  const [์ปดํฌ๋ํธ๋ช] = style.[htmlํ๊ทธ]`
    [๋ถ์ฌํ๊ณ ์ ํ๋ css์์ฑ]
  `;
  ```
  ๐กย ์ฐธ๊ณ  [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals)

### > ์คํ์ผ ์ปดํฌ๋ํธ์ ํ์ฉ

๐กย ๊ณต์๋ฌธ์ : [https://styled-components.com/](https://styled-components.com/)

### **๐ฆย props**

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

- props๋ก ์กฐ๊ฑด์ ๋ฐ๋ฅธ ์คํ์ผ๋ง์ ๋์ ์ผ๋ก ํ  ์ ์๋ค.

### **๐ฆย ์์ ์คํ์ผ**

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

- ์ด๋ฏธ ์ ์ธ๋ ์คํ์ผ๋ ์ปดํฌ๋ํธ๋ฅผ ํ์ฉํ์ฌ ์๋ก์ด ์คํ์ผ๋ ์ปดํฌ๋ํธ๋ฅผ ๋ง๋ค ์ ์๋ค.
- NewButton ์ปดํฌ๋ํธ์๋ Button ์ปดํฌ๋ํธ์ ์ ์ฉํ ์คํ์ผ์ด ๊ทธ๋๋ก ์์๋์ด ์ถ๊ฐ๋ก ์ ์ฉํ ์คํ์ผ ์ด์ธ์๋ ๊ฐ์ ์คํ์ผ์ด ์ ์ฉ๋๋ค.

```jsx
// App.js

import { Link } from "react-router-dom";
import styled from "styled-components";

const App = () => {
  return <CartLink to="/cart">์ฅ๋ฐ๊ตฌ๋</CartLink>;
};

const CartLink = styled(Link)`
  color: red;
`;

export default App;

// Elements

<a class="sc-eCYdqJ gubPie" href="/cart">
  ์ฅ๋ฐ๊ตฌ๋
</a>;
```

- ๊ฐ์ ํ์ผ์์ ์ ์ธํ ์คํ์ผ๋ ์ปดํฌ๋ํธ๋ฟ๋ง ์๋๋ผ, Link, ์์ด์ฝ ๋ผ์ด๋ธ๋ฌ๋ฆฌ ๋ฑ ์ธ๋ถ ๋ผ์ด๋ธ๋ฌ๋ฆฌ ์ปดํฌ๋ํธ๋ import ํ๋ฉด ์์ ์์์ฒ๋ผ ์คํ์ผ์ ํ์ฅํ์ฌ ์ฌ์ฉ ๊ฐ๋ฅํ๋ค.

### **๐ฆย ๋ค์คํ**

์๋์ ๊ฐ์ด ๋ค์คํํด์ ์คํ์ผ์ ์ ์ฉํ  ์ ์๋ค.

```jsx
import React from "react";
import styled from "styled-components";

const Main = () => {
  return (
    <List>
      <li>
        ๋ฉ๋ด<a href="http://list">ํด๋ฆญ</a>
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

**But !!** ์คํ์ผ๋ ์ปดํฌ๋ํธ๋ **์ปดํฌ๋ํธ๋ฅผ ๋ถ๋ฆฌํด์ ๋ชจ๋ํํ๊ธฐ ์ํด ์ต์ ํ** ๋์ด์๊ธฐ ๋๋ฌธ์, **๋ค์คํ**์ ์ ์ฉํด์ ์ฌ์ฉํ๋ ๊ฒ๋ณด๋ค **ํ๋์ ์ปดํฌ๋ํธ๋ก ๋ถ๋ฆฌ**ํด์ ์ฌ์ฉํ๋ ๊ฒ์ด ๋ ์ข๋ค.

๋ค์คํ์ ์ฌ์ฉํด์ผ ํ๋ ๊ฒฝ์ฐ

```jsx
import React from "react";
import styled from "styled-components";
import Slider from "react-slick";
import "slick-carousel/slick/slick.css";
import "slick-carousel/slick/slick-theme.css";

const Main = () => {
  return <Carousel>// slick ์ฝ๋</Carousel>;
};

const Carousel = styled(Slider)`
  .slick-slide {
    // slick ์ปค์คํ ์คํ์ผ
  }
`;

export default Main;
```

- react-slick๊ณผ ๊ฐ์ ์ธ๋ถ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ์ฌ์ฉํ์ฌ ์ด๋ฏธ ์ ํด์ง ์คํ์ผ์ ๋ณ๊ฒฝํด์ผ ํ  ๋๋ ๋ค์คํ์ ์ด์ฉํด์ ์คํ์ผ๋ง์ ํด์ผํ๋ค.

### **๐ฆย ๊ณตํต์คํ์ผ**

### **1. GlobalStyle**

common.css ์ฒ๋ผ ์ ์ญ์ ๊ณตํต์ผ๋ก css ์คํ์ผ์ ์ ์ฉํด์ฃผ๋ ๋๋ ์๋ค.

**createGlobalStyle** ํจ์๋ฅผ ํตํด **์ ์ญ์ ์ ์ฉ**ํ๊ธฐ ์ํ ์คํ์ผ ์ปดํฌ๋ํธ๋ฅผ ์์ฑํ  ์ ์๋ค.

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

๐

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

- createGlobalStyle ํจ์๋ก ์์ฑํ GlobalSyle ์ปดํฌ๋ํธ๋ฅผ ์ ์ญ์คํ์ผ์ ์ ์ฉํด์ฃผ๊ณ  ์ถ์ ์ปดํฌ๋ํธ ์์์ ์ ์ฉํด์ฃผ๋ฉด ํ์ ์ปดํฌ๋ํธ์ ์ ์ฉ๋๋ค.

### **2. styled-reset**

reset.css ์ฒ๋ผ ๊ธฐ๋ณธ ์คํ์ผ์ ์ด๊ธฐํ ํด์ฃผ๋ ์์์ GlobalStyle.js ํ์ผ์ ์ ์ธํ์ฌ ์ ์ญ์ ์ ์ฉํ  ์ ์๋ค.

1. ์ค์น

   ```jsx
   $ npm install styled-reset
   ```

2. ์ ์ธ๋ฐฉ๋ฒ (createGlobalStyle``; ์์ ${reset}์ ์ ์ธํด์ค๋ค.)

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

sass์์๋ ๋ณ์์ mixin ๋ฑ ๊ณตํต์ผ๋ก ์ฌ์ฉํ  ์คํ์ผ์ ๋ํด์ ํ์ผ์ ๋ง๋ค๊ณ , ์ฌ์ฉ ํ๊ณ ์ ํ๋ scss ํ์ผ์ import๋ฅผ ํด์ ์ ์ฉ ์์ผฐ๋ค. ํ์ง๋ง ๋งค๋ฒ import๋ฅผ ํด์ฃผ๊ณ , ์ฐธ์กฐํด์ผ ํ๋ css ํ์ผ์ด ๋ง์์ง๋ฉด ์์กด์ฑ์ ๊ด๋ฆฌํ๊ธฐ๋ ํ๋ค์ด์ง๋ค.

โ ์ด๋ฐ ๋ฌธ์ ๋ฅผ ํด๊ฒฐํ๊ธฐ ์ํด์ ์คํ์ผ ์ปดํฌ๋ํธ์์๋ ThemeProvider๋ฅผ ํตํด ์ ์ญ์ผ๋ก ํ๋ง, JS๋ณ์ ๋ฑ์ ๊ณต์ ํ์ฌ ์ฌ์ฉํ๋ค.

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

- ThemeProvider๋ ์์ ์์์ ๊ฐ์ด ํ๋ก์ ํธ์ ์ํธ๋ฆฌ ํฌ์ธํธ์ธ index.js์ ์ต์ด๋ก ๋ ๋๋ง ๋๋ ์ปดํฌ๋ํธ๋ฅผ ๊ฐ์ธ์ฃผ์ด์ ๋ชจ๋  ์ปดํฌ๋ํธ์ prop์ theme์ ๋ถ์ฌํ์ฌ ์ ์ฉํ  ์ ์๋ค.

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

- color, fontSize๋ฑ ๊ณตํต๋ ํ๋ง๋ theme.js์์ ์ ์ธํ์ฌ ๊ฐ ์ปดํฌ๋ํธ์์ props๋ก ๋ฐ์ ์คํ์ผ์ ์ ์ฉํ  ์ ์๋ค.
- ThemeProvider์ ์์ฑ์ผ๋ก ๋๊ฒจ์ฃผ๋ฉด ์ ์ญ์์ ์ฌ์ฉ๊ฐ๋ฅ

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

// console.log(props)์ ๊ฒฐ๊ณผ

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

- ์ ์ญ์ ์ผ๋ก ์ฌ์ฉํ๊ธฐ ์ํ theme.js ํ์ผ์ ๋ง๋ค๊ณ , ํด๋น ํ์ผ์ index.js์์ ThemeProvider๋ฅผ ํตํด ์ค์ ํด ์ฃผ๋ฉด, ์์ ์์์ฒ๋ผ props๋ก ๋ฐ์์์ ์ฌ์ฉํ  ์ ์๋ค.
- ์ด๋ค ํํ๋ก ๋ค์ด์ค๋์ง console.log ๋ก ํ์ธ์ ํด๋ณด๋ฉด props๋ ๋ค์๊ณผ ๊ฐ์ ๊ฐ์ฒด ํํ๋ก ๋ฐ์ดํฐ๊ฐ ๋ค์ด์ค๊ฒ ๋๋ค. ๊ทธ๋์ props.theme.ligthrgrey๋ก ๊ฐ์ ์ฌ์ฉํ  ์๊ฐ ์๊ฒ ๋๋ค ๐

**2. mixin**

์์ฃผ ์ฌ์ฉํ๋ css ์คํ์ผ์ ๋ํด์๋ variables.js ํ์ผ์ ๋ณ๋๋ก ์์ฑํ์ฌ ์ฌ์ฉํ๋ ๊ฒ์ด ์ข๋ค.

variables.js ํ์ผ์ theme๊ณผ variables๋ฅผ Theme Provider์ ๊ฐ์ด prop์ผ๋ก ํฉ์ณ์ ์ ์ญ์์ ์ฌ์ฉํ๊ฑฐ๋, ์ฌ์ฉํ๊ณ ์ ํ๋ ํ์ผ์์๋ง importํด์ mixin์ ์ฌ์ฉํ  ์ ์๋ค.

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

- **ThemeProvider์์ prop์ผ๋ก ํฉ์ณ์ ์ฌ์ฉ**

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

  ์ฌ์ฉํ  ๋๋ ๋ค์๊ณผ ๊ฐ์ด ์ ์ฉ!

  ```jsx
  // App.js

  const App = () => {
    return (
      <Container>
        <Button>์ฒซ๋ฒ์งธ ๋ฒํผ</Button>
        <Button>๋๋ฒ์งธ ๋ฒํผ</Button>
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

  variables.js ํ์ผ์์ ๊ธฐ๋ณธ์ผ๋ก ์ค์ ํ ๊ฐ์ ์ฌ์ฉํ  ๋๋ flexSet()์ ์จ์ฃผ๊ณ , ๋ค๋ฅธ ์ธ์๋ฅผ ๋๊ฒจ์ค๋๋ `${(props) => props.theme.variables.flexSet(โโ,โspace-betweenโ,โcenterโ)}` ์ฒ๋ผ ์ ์ฉํ๊ณ  ์ถ์ ์ธ์๋ฅผ ๋๊ฒจ์ค ์ ์๋ค.

- **๊ฐ ์ปดํฌ๋ํธ์์ variables.js ํ์ผ์ importํด์ ์ฌ์ฉ**

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

### 4. ๊ธ๋ก๋ฒ ํฐํธ

์ ์ญ์์ ์ฌ์ฉํ๊ธธ ์ํ๋ฉด GlobalStyle.js์ body์์ font-family๋ฅผ ์น ํฐํธ ๋ช์ผ๋ก ์ง์ ํด์ฃผ์ด์ผ ํ๋ค.

์น ํฐํธ๋ฅผ ์ฌ์ฉํ  ๊ฒ์ธ์ง, ํฐํธ ํ์ผ์ ์ฌ์ฉํ  ๊ฒ์ธ์ง์ ๋ํด์ ์ค์ ๋ฐฉ๋ฒ์ด ๋ฌ๋ผ์ง๋ค.

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

1. **์น ํฐํธ**

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

   - ์น ํฐํธ ์ฌ์ฉํ  ๋๋ ์น ํฐํธ ์ฌ์ดํธ์์ ์ ๊ณตํ๋ embedding(์๋ฒ ๋) ์ฝ๋๋ฅผ ๋ณต์ฌํ์ฌ html ํ์ผ์ ์ฝ๋๋ฅผ ์ถ๊ฐํด์ผ ํ๋ค.
   - index.html์ head์์ link ํ๊ทธ๋ฅผ ์ด์ฉํด์ ๊ธ๋ก๋ฒ ํฐํธ๋ก ์ง์ ํด์ ์ฌ์ฉํ  ์ ์๋ค.

2. **ํฐํธํ์ผ**

   ```jsx
   src
   โโโ styles
       โโโ fonts
       โย ย  โโโ DoHyeon-Regular.ttf
       โโโ GlobalFont.js
       โโโ GlobalStyle.js
       โโโ theme.js
   ```

   - styles ํด๋ ์์ ํฐํธํ์ผ์ ์ ์ฅํ  ํด๋๋ฅผ ์์ฑํ์ฌ ํฐํธํ์ผ์ ๋ฃ์ด์ค๋ค.

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

   - ์คํ์ผ๋ ์ปดํฌ๋ํธ์ createGlobalStyle์ ํตํด ๊ธ๋ก๋ฒ ์คํ์ผ์ ์์ฑํด์ค๋ค. ์ด ๋ @font-face๋ฅผ ์ฌ์ฉํ์ฌ ์น ํ์ด์ง์ ์ ์ฉ ๊ฐ๋ฅ

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

   - ์ ์ญ์์ ์ฌ์ฉํ๊ธฐ ์ํด์๋ ์์ ๊ฐ์ด ์ ์ฉํด์ ์ฌ์ฉ!
