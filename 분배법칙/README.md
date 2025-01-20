## 분배법칙

타입스크립트에서 조건부 타입(conditional type)이 `유니온 타입`에 적용 될 때는 자동으로 `분배법칙`이 적용된다. <br/>

```js
type Foo = 'a' | 'b' | 'c';
type A = MyExclude<Foo, 'a'>;
```

위 코드에서 실제로 일어나는 일은 이렇다.

```js
('a' extends 'a' ? never : 'a') |
('b' extends 'a' ? never : 'b') |
('c' extends 'a' ? never : 'c')
```

즉, `[P in T]`와 같은 mapped type을 사용하지 않아도, TypeScript는 자동으로 유니온의 각 멤버에 대해 조건을 검사한다. <br/>

참고로 mapped type `[P in T]`는 객체 타입을 만들 때 사용된다.

```js
// 이건 객체 타입을 만들 때 사용하는 방식
type Example = {
  [P in 'a' | 'b' | 'c']: string
}

// 결과:
{
  a: string;
  b: string;
  c: string;
}
```
