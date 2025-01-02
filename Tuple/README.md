# Tuple 타입

> 튜플 타입은 Typescript에서 배열의 구조를 좀 더 엄격하게 정의할 수 있게 해준다.

- 튜플 타입은 `길이가 고정`되어 있다.
- 각 위치의 타입이 명확히 `지정`되어 있다.

```js
const person = {
  name: 'Test',
  age: 30,
  role: [2, 'author'], // role:(number|string)[] 로 타입 추론이 되어있는 상태다.
};

person.role.push('admin');
```

타입스크립트는 우리가 두 개 요소만 원한다는걸 알지 못한다.
그렇기 때문에 아래와 같은 상황도 통과시킨다.

```js
person.role.push('admin');
person.role[1] = 10;
```

이런 상황을 방지하고자 쓰는게 `Tuple` 타입이다.

# Tuple 적용

```js
const person = {
  name: 'Test',
  age: 30,
  role: [2, 'author'] as [number,string],
};
```
