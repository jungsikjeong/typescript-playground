# infer

> 조건부 타입에서 미리 정의되지 않은 타입을 유연하게 정의할 수 있게 도와주는 문법이다.<br/>
> 항상 조건부 타입 문법과 같이 사용되며, 복잡한 타입 코드를 줄여준다.

## 예시

```js
type ElementType<T> = T extends (infer U)[] ? U : T
```

- 위의 예시 코드는 아래 코드와 같다.

```js
type ElementType<T> = T extends string[] ? string : T;
type ElementType<T> = T extends number[] ? number : T;
type ElementType<T> = T extends boolean[] ? boolean : T;
type ElementType<T> = T extends never[] ? never : T;
```

- `"대략적으로 이런 형상의 데이터가 들어올 거니 취급해줘"` 가 바로 infer 키워드의 역할이다.

## 함수 반환 타입 추론

> 반환 타입이 지정된 함수를 제네릭 타입에 넘기면 반환 타입을 알 수 있다.

예시

```js
type ReturnTypeOf<F> = F extends () => infer R ? R : never;

type Result = ReturnTypeOf<() => boolean>; // boolean
type Result = ReturnTypeOf<() => string>; // string

```

함수에 파라미터가 있거나 함수가 아닌 타입에 대해서는 `never`을 리턴함

```js
type Result = ReturnTypeOf<(a: string) => boolean>; // never
type Result = ReturnTypeOf<number>; // never
```
