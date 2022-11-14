# Portals을 활용한 모달 (Semantic한 HTML 코드)

## 리액트 Portals

```jsx
return (
  <>
    <Modal />
    <InputForm />
  </>
);
```

위의 코드는 모달과 폼으로 이루어져 있다.

별 문제 없어 보이지만

```jsx
<section>
  <h1>Dashboard</h1>
  <div className="modal">
    <span>this is modal!!</span>
  </div>
  <form>
    <input type="text" />
  </form>
</section>
```

이와 같이 semantic한 관점이나 간결한 HTML 구조를 갖췄는지를 따져보면

별로 좋지 않은 코드이다.

왜? 모달의 기본적인 역활은 페이지 위에 표시되는 오버레이이기 때문

모달은 페이지 전체의 대한 오버레이이므로 모든 것 위에 있다.

그래서 만약 모달이 다른 HTML 안에 중첩돼 있다면 styling을 하여 작동을 할지는 몰라도 좋은 코드, 구조는 아닌 것!!

문제가 생길 수 있는 부분은 예를 들어 스크린 리더가 렌더링 되는 HTML 코드를 해석할 때 오버레이 내용이 중첩되어 있다면 일반적인 오버레이라고 인식 못할 수도 있다.

⇒ CSS styling은 그다지 큰 역할을 하지 않기 때문이다.

또한 semantic한 관점이나 구조적인 관점에서 이것은 HTML 코드 안 깊은 곳에 자리잡고 있고 이 모달이 다른 모든 내용에 대한 오버레이인지 명확하지가 않다.

HTML, CSS, JavaScript는 유연하여 많은 것을 작동하도록 할 수 있지만, 작동 한다는 이유만으로 좋은 구현이라고는 할 수 없다.

<br />

### 그럼 modal에 대해 좋은 구현을 어떻게 할까?

<br />

React의 Portal을 이용하여 계속 원하는 대로 컴포넌트를 작성하고 데이터를 전달할 때 마찰이 없도록 구조를 유지할 수 있다.

Portal은 두 가지가 필요하다.

1. **컴포넌트를 이동시킬 장소**

   ```jsx
   // index.html
   <body>
     <div id="backdrop-root"></div>
     <div id="overlay-root"></div>
     <div id="root"></div>
   </body>
   ```

   - root div 위에 두 개의 div를 추가한다.
   - “backdrop-root” 밑에 “overlay-root”는 모든 종류의 오버레이를 가져올 수 있다.

<br />

2. **컴포넌트에게 그 장소에 포털을 가져야 한다고 알려줘야 한다.**

   ```jsx
   const ErrorModal = (props) => {
     return (
       <div>
         <div className={classes.backdrop} onClick={props.onConfirm} />
         <Card className={classes.modal}>
           <header>
             <h2>{props.title}</h2>
           </header>
           <div>
             <p>{props.message}</p>
           </div>
           <footer>
             <Button onClick={props.onConfirm}>confirm</Button>
           </footer>
         </Card>
       </div>
     );
   };
   ```

   👇

   ```jsx
   import ReactDOM from "react-dom";

   const Backdrop = (props) => {
     return <div className={classes.backdrop} onClick={props.onConfirm} />;
   };

   const ModalOverlay = (props) => {
     return (
       <Card className={classes.modal}>
         <header>
           <h2>{props.title}</h2>
         </header>
         <div>
           <p>{props.message}</p>
         </div>
         <footer>
           <Button onClick={props.onConfirm}>confirm</Button>
         </footer>
       </Card>
     );
   };

   const ErrorModal = (props) => {
     return (
       <>
         {ReactDOM.createPortal(
           <Backdrop onConfirm={props.onConfirm} />,
           document.getElementById("backdrop-root")
         )}
         {ReactDOM.createPortal(
           <ModalOverlay
             title={props.title}
             message={props.message}
             onConfirm={props.onConfirm}
           />,
           document.getElementById("overlay-root")
         )}
       </>
     );
   };
   ```

   - 상수로 선언한 Backdrop은 오버레이 뒤 검은 배경
   - ModalOverlay에 모달안의 내용이 들어온다.
   - 리액트 DOM은 브라우저에 대한 리액트용 어댑터의 일종이라 할 수 있다.
     ⇒ react-dom을 import한다. ⇒ createPortal 메소드 호출가능
   - createPortal 메소드는 두 개의 인수를 가진다.
     - 렌더링되어야 하는 리액트 노드 (<Backdrop/>)
     - 실제로 렌더링되어야 하는 요소 (DOM API 사용)

<br />

위의 과정과 같이 Portal의 핵심은 JSX 코드 안에서 렌더링된 HTML 내용을 다른 곳으로 옮기는 것이다.

이 HTML 코드는 다른 위치에서 렌더링되고 이전의 modal을 사용하던 것 처럼
커뮤니케이션이 가능하다.

이러한 기능들을 활용하여 더 semantic한 HTML 코드를 쓸 수 있다.

---
