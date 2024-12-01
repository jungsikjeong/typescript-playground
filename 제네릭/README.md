# 제네릭

> 제네릭은 타입을 `파라미터처럼` 받아서 사용하는 방식이다.
> 함수나 클래스 등에서 여러 타입을 유연하게 처리할 수 있게 해준다.

## 주요 특징

- 타입 안전성을 보장하면서 재사용 가능한 코드를 작성할 수 있다

- 컴파일 시점에 타입 검사가 이루어진다

- 다양한 데이터 타입에 대해 동작하는 컴포넌트를 만들 수 있다

## 자주 사용되는 상황:

- 배열이나 프로미스 같은 컨테이너 타입을 다룰 때

- API 응답 처리할 때

- 범용 유틸리티 함수를 만들 때

- 컴포넌트의 props 타입을 정의할 때

## 제약 조건(constraints)

> 제네릭 타입이 가져야 할 속성 지정 가능

```js
interface HasLength {
    length: number;
}

function printLength<T extends HasLength>(arg: T): number {
    return arg.length;
}

printLength("hello");     // 가능
printLength([1, 2, 3]);   // 가능
// printLength(123);      // 오류: number에는 length 속성이 없음
```

- 사실 위에서 `T extends HasLength` 대신 `T[]로 배열로 지정`하는 방법도 있으나, 이 경우 두 가지 단점있음

  - 첫째, 유니언 타입으로 처리하면 코드가 불필요하게 길어지고 복잡해짐
  - 둘째, T[]로 제네릭을 배열로 지정하면 배열만 받을 수 있어서 "hello"와 같은 문자열은 처리할 수 없게 됨. 반면 `T extends HasLength`를 사용하면 length 속성을 가진 모든 타입을 깔끔하게 처리할 수 있게됨.
