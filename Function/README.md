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

한단계 🆙! <br/>
추가로 제네릭 타입에서 함수 타입만 들어오게끔 제약하게 하고싶다면<br/>
이런식으로도 사용가능하다

```js
type 함수만와<T extends (...args: any) => any> = T

// 가능
type Test1 = 함수만와<(x: string) => void>;  

// 컴파일 에러
type Test2 = 함수만와<string>;
type Test3 = 함수만와<{ a: string }>;
```

> 제네릭에서의 `extends`는 할당 가능한가?를 체크한다!
