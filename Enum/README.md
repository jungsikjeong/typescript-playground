# Enum

> `열거형` 타입이다.
> 코드의 가독성과 유지보수성을 높이는데 도움을 준다.

- 상수들의 집합을 정의 할 수 있다.
- 기본적으로 0부터 시작하는 숫자형 값이 할당된다.

  - 자동으로 시작 값에서 1씩 더해서 값을 할당한다.

- 각 상수에 직접 값을 할당 할 수 있다.

```js

enum Role {
  ADMIN, // 0이 할당되어있다.
  READ_ONLY,  // 1
  AUTHOR // 2
}

const person ={
  name:'join',
  age:30,
  ...
  role:Role.ADMIN
}
```

- 직접 값을 할당해 줄 수 있다.
- 텍스트를 할당해 줄 수 있다.

```js
enum Role {
  ADMIN = 5,
  READ_ONLY ='READ_ONLY',
  AUTHOR // 2
}
```
