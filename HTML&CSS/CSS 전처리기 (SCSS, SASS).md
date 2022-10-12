# CSS 전처리기 (SCSS, SASS)

## SASS 개념

> **Syntactically Awesome Style Sheets : 문법적으로 어썸한 스타일 시트!!**
- Sass는 세계에서 가장 성숙하고 안정적이며 강력한 전문가 급 CSS 확장 언어
- Sass는 기초 언어에 힘과 우아함을 더해주는 CSS의 확장
> 

🤔 웹 페이지가 점점 커지면서 CSS 코드도 굉장히 많아지게 되고 유지 보수 하기 어려운 점이 생길 수 있다.

😃 CSS를 **Awesome** 하게 만들어 줌으로써 개발 과정에서 좀더 편하게 코딩할 수 있다! 

 

Sass는 CSS 전처리기 (Preprocessor)라고 한다. 

CSS 전처리기 : 기존 css가 가질 수 있는 불리한 점을 해결하기 위해 탄생하였다. 

💡 참고하면 좋은 사이트 : [https://sass-guidelin.es/ko/](https://sass-guidelin.es/ko/)

## SASS의 장단점

### 장점

- 확장성 : Sass 기반의 프레임워크가 다수 존재
- 신뢰도 : 거대 커뮤니티의 지원 아래 개발되고 있다.
- 인지도 : 업계에서 인정받고 있고, 많이 사용되고 있다.
- 안정성 : 오랜 기간 적극적인 지원 아래 관리되어 왔다.
- 기능성 : 다양한 기능을 제공하고, 거의 모든 면에서 뛰어나다.
- 호환성 : 모든 버전의 CSS와 완벽하게 호환된다.

👉 **뛰어난 생산성!!** 

CSS를 마치 프로그래밍 하듯이 코딩할 수 있고 빠른 시간 안에 간결하게 작성할 수 있게 해준다.

### 단점

- 웹에서는 CSS만 동작하기 때문에 전처리기는 직접 동작시킬 수가 없다.
→ CSS로 컴파일 후 동작시켜야 한다.
- 전처리기를 위한 도구가 필요하다 → 다시 컴파일하는 시간이 느릴 수 있다.
- 노드 버전을 바꿀 때 자주 다시 컴파일 해야한다.

## SASS, SCSS

SCSS는 구문이다. SCSS 문접을 기반으로 코드를 작성하면 Sass 전처리기의 도움을 받아 컴파일러가 이를 CSS로 빌드할 수 있다.

SCSS = Sass 문법만 살짝 다르다! **Sass**는 **‘SCSS 구문을 사용하는 것’**

```jsx
// SCSS
$theme-color: blue;

@mixin title($color) {
    font-size: 20px;
    color: $color;
}

#header {
    @include title($theme-color);
}
```

```jsx
// Sass
$theme-color: blue

=title($color)
     font-size: 20px;
     color: $color

#header
   +title($theme-color)
```

👉 기존 Sass 구문은 들여쓰기 문법을 사용 → 새로 나온 SCSS 구문은 대괄호와 세미콜론을 사용하여 좀 더 친숙하게 사용 가능하다.

## SASS 도입기

**1. 설치**

💡 .scss 파일을 만들고 이걸 그대로 서버에 올리면 웹 브라우저는 이해할 수 없다!

👉 SCSS를 브라우저가 읽을 수 있는 코드(CSS)로 바꿔줘야 한다. (이를 ‘컴파일’ 이라고 하며, 컴파일을 하기 위해선 ‘컴파일러’ 설치가 필요하다.)

```jsx
npm install sass --save
```

- 설치 시 node-modules 폴더에 sass 폴더가 생성된다.
- —save : package.json에 설치된 패키지의 이름과 버전 정보를 업데이트!

```jsx
// package.json
{
  "name": "westagram-react",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@testing-library/jest-dom": "^4.2.4",
    "@testing-library/react": "^9.3.2",
    "@testing-library/user-event": "^7.1.2",
    "sass": "^4.14.1",
    "react": "^16.13.1",
    "react-dom": "^16.13.1",
    "react-scripts": "3.4.3"
  }
}
```

**2. .css 파일의 확장자를 .scss로 바꾸기**

Sass 파일의 확장자는 ‘.scss’ 이다. 

‘.css’ 확장자로 되어 있는 파일을 전부 ‘.scss’ 확장자로 바꿔준다.
(자바스크립트 파일의 import 구문도 수정!)

**3. Nesting 기능 적용하기**

Sass의 가장 기본적인 기능으로 Nesting 이라는 것이 있다.

JSX 최상위 요소의 ‘className’을 컴포넌트 이름과 동일하게 설정해주고, 

‘.scss’ 파일에서도 최상위 요소 안 쪽에서 하위 요소의 스타일 속성을 정의할 수 있다.

```jsx
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav li {
  display: inline-block;
}

nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

👇

```jsx
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;

      li {
        display: inline-block;
      }
    }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

**4. 변수 활용, & 연산자, mixin 등 기본 기능 적용하기**

```jsx
.login-container {
  display: flex;
  justify-content: center;
  align-items: center
}

button {
  width: 200px;
  height: 100px;
  background-color: blue;
}

button:hover {
  background-color: red;
  cursor: pointer; 
}
 
input {
  background-color: blue;
}

input:focus {
  background-color: red;
}
```

👇

```jsx
$theme-color: blue;
$border-style: 1px black solid;

@mixin flex-center {
  display: flex;
  justify-content: center;
  align-items: center
}

.login-container {
  @include flex-center;

  button {
    width: 200px;
    height: 100px;
    background-color: $theme-color;

    &:hover {
      background-color: red;
      cursor: pointer;
    }
  }

  input {
    background-color: $theme-color;

    &:focus {
      background-color: red;
    }
  }
}
```

💡참고

[https://nykim.work/97](https://nykim.work/97)

[https://penguingoon.tistory.com/275](https://penguingoon.tistory.com/275)