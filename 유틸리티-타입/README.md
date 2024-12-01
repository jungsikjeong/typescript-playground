> 계속 추가 예정! (타입스크립트 공홈에 나와있는걸 보고 이해한걸 적을 예정)
> [공홈](https://www.typescriptlang.org/docs/handbook/utility-types.html)

## Partial

> 모든 속성을 옵셔널 타입으로 만든다.

### 주의점

> 객체 내부 속성은 옵셔널로 변환이 안됌

```js
interface NestedTodo {
    title: string;
    description: string;
    author: {
        name: string;
        email: string;
    }
}

// author 객체의 내부 속성은 여전히 필수
type PartialNestedTodo = Partial<NestedTodo>;


// 깊은 Partial이 필요한 경우
type DeepPartial<T> = {
    [P in keyof T]?: T[P] extends object ? DeepPartial<T[P]> : T[P];
};

type DeepPartialNestedTodo = DeepPartial<NestedTodo>;

```

## Readonly

> 읽기 전용이라고 타입스크립트에게 알려주는 기능

```js
const names: Readonly<string[]> = ['테스트1', '테스트2'];
names.push('테스트3'); // 타입스크립트가 에러를 띄움
```
