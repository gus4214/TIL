# forEach와 map 메서드의 차이

> forEach와 map은 JavaScriopt에서 배열 형태의 데이터를 순회할 때 많이 쓰이는 array method로 잘 활용 한다면 짧고 직관적인 로직구현이 가능하다.

😃 forEach와 map 메서드는 동일하게 파라미터로 콜백 함수를 받는다.

-> 콜백 함수의 파라미터 : **요소**, **index**, **배열 그 자체**

(일반적으로 첫 번째 요소와 두 번째 index가 많이 사용된다.)

😃 forEach와 map 메서드는 배열을 순회하며 파라미터로 전달한 원소의 값을 가지고 함수 로직을 구현한다는 것에서 공통점이 있다.

→ **하지만 근본적으로 return 하는 값이 있는지 / 없는지에서 차이가 있다.**

- forEach 메서드를 사용하여 원소 값을 각각 +1씩 증가

```jsx
let numData = [ 1, 2, 3, 4, 5 ];

let newNumData = [];

numData.forEach(num => {newNumData.push(num + 1)};

console.log(newNumData); // [ 2, 3, 4, 5, 6]
```

- map 메서드를 사용해서 원소 값을 각각 +2씩 증가

```jsx
let numData = [1, 2, 3, 4, 5];

let newNumData = numData.map((num) => {
  return num + 2;
});

console.log(newNumData); // [ 3, 4, 5, 6, 7]
```

> MDN Search <br>
> forEach는 return value가 undefined <br>
> map은 콜백 함수의 결과 값들로 구성된 새로운 배열을 return

👉  forEach는 map메서드와 다르게 콜백 함수가 return 하는 값을 따로 모아서 어떤 처리를 하는 과정이 없기 때문에, 메서드를 호출한 코드를 함수에 할당하면 undefined가 할당된다.

따라서 forEach 메서드는 변수에 할당하기 보다는 반복문이나 조건문과 같이 그냥 바로 호출되는 것이 일반적이다.

- 배열을 순회하며 원소의 값들을 각각 가공하여 새로운 배열을 return 받고자 한다면 map 메서드를 사용
- 원소의 값들을 활용해서 원소들의 합이나, 평균 그리고 원래 배열과 길이가 다른 배열 결과를 받고자 한다면 forEach 메서드를 사용
