# Function

> 함수의 타입을 정의하는데 사용되는 타입
> 매개변수와 함수의 반환 값 까지 정의 가능함.

개인적으로 리액트로 props로 함수를 받을때, 그냥 그렇게 했어야했어서 아무 생각없이 사용했었던 타입이였는데, 이런게 타입스크립트에 있었다니 좀 충격이였음..

```js
let multiply: (a: number, b: number) => number; // 타입 정의

multiply = function (x: number, y: number): number {
  return x * y;
};
```
