# 인덱스 시그니처

- 속성 이름을 미리 알지 못해도 유연하게 대응이 가능하다.
- 인덱스 시그니처는 `미리 정해지지 않은 객체의 속성 타입을 정의할 때 사용`하면 좋다.
```js
interface ErrorContainer {
  [prop: string]: string;
}

const errorBag: ErrorContainer = {
  email: 'Not a valid email!',
  username: 'Must start....',
};

// key 값에 email 대신에 숫자를 써도 된다.
// string타입으로 추론된다.
const errorBag: ErrorContainer = {
  1: 'Not a valid email!',
  username: 'Must start....',
};
```
