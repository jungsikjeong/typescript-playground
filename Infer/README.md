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

# 템플릿 리터럴 타입에서의 패턴 매칭

> 기본 패턴

```js
// 첫 글자 가져오기
type FirstChar<T extends string> = T extends `${infer F}${infer R}` ? F : never;

// 예시:
type A = FirstChar<'BFE'> // 'B'
type B = FirstChar<'dev'> // 'd'
type C = FirstChar<''> // never
```

> 패턴 매칭의 동작 방식
<br/>

TypeScript는 패턴 매칭 시 반환하는 값에 따라 다르게 동작함!


```js
// 마지막 글자 가져오기
type GetLast<T extends string> = T extends `${infer R}${infer L}` ? L : never;
// 'Hello' -> R='Hell', L='o'

// 첫 글자 가져오기
type GetFirst<T extends string> = T extends `${infer R}${infer L}` ? R : never;
// 'Hello' -> R='H', L='ello'

```

- 조건문의 반환값(? L vs ? R)에 따라 패턴 매칭 방식이 달라진다.
- L을 반환할 때는 `R`이 탐욕적으로 매칭됨
- R을 반환할 때는 `R`이 최소한으로 매칭됨

<br/>

여기서 `탐욕적`이라는것은 최대한 많이 값을 가져간다로 이해하면 된다.<br/>
위의 예제 중 마지막 글자 가져오기에서 조건문의 반환타입이 마지막 infer인 `L` 이였는데, 이때는 앞에 infer R이 최대한의 값을 많이 가져가고,<br/>
첫 글자 가져오기에서 조건문의 반환타입이 첫번째인 R로 되어있다. 이때는 뒤에있는 infer L이 나머지들을 탐욕적이게 가져가고 R이 첫번째 글자 하나만 가져가게된다.
