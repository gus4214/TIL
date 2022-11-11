# JSX 코드에서 조건부 내용 가독성있게 출력하기

```jsx
return (
  <div>
      <Card>
        {filterdData.length === 0 && <p>No Data</p>}
        {filterdData.length > 0 &&
          filterdData.map((data) => {
            return (
              <Cardbox
                key={data.id}
                title={data.title}
                date={data.date}
              />
            );
          })}
      </Card>
  </div>
)
```

위와 같이 필터링된 데이터를 활용하여 화면에 출력하고자 할 때 JSX코드 내에서 && 연산자를 활용할 수 있다.

👇 

하지만, 변수에 JSX 컨텐츠를 저장하고 이 값을 사용하여 변환하고 사용할 수 있다. 
변수에 저장되는 값을 생성하는데도 JSX코드는 제한없이 사용할 수 있다. 

JSX코드 에서 로직을 제거하고 심플하게 동적 표현식을 넣어줄 수 있다. 

컴포넌트 함수 자체에 로직을 가지게 하여 더 가독성이 좋고 깔끔한 JSX코드를 작성 할수 있다.

```jsx
// React.js

let dataContent = <p>No Data</p>;

if (filterdData.length > 0) {
    dataContent = filterdData.map((data) => {
      return (
         <Cardbox
           key={data.id}
           title={data.title}
           date={data.date}
         />
      );
    });
  }

return (
  <div>
      <Card>
        {dataContent}
      </Card>
  </div>
)
```