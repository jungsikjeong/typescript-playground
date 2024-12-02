# keyof

> 객체 타입의 모든 키를 추출하는 연산자다.

## 주요 특징

- 객체 타입을 받아 객체의 key들로 구성된 문자열 또는 숫자 유니온 타입을 생성한다.
- 제네릭과 함께 사용하면 더욱 강력한 타입 체크 가능하다.
- 타입 안전성을 보장하면서 객체의 속성에 접근 가능하다.

## 예시

```js
//  인덱스 타입과 함께 사용
type StringMap = { [key: string]: unknown };
// StringMapKeys는 string 타입이 됨
type StringMapKeys = keyof StringMap;

// 배열과 함께 사용
type ArrayKeys = keyof [];
// 'length' | 'toString' | 'pop' | 'push' | ... 등의 배열 메서드와 속성들의 유니온 타입이 됨

// 클래스와 함께 사용
class Dog {
    name: string;
    age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
}

// DogKeys는 'name' | 'age' 타입이 됨
type DogKeys = keyof Dog;
```

## 실제 적용사례 (위의 예시보다는 좀 더 와닿음)

```js

// Before(keyof 적용 전)
function extractAndConvert (obj:object,key:string){

  return 'Value :' + obj[key]
}


// After
// 두번째 매개변수로 오는 key가 첫번째 타입의 속성이라는걸 확실히 알려줌
function extractAndConvert<T extends object, U extends keyof T> (obj:T,key:U){

  return 'Value :' + obj[key]
}


// 근데 막상 사용하면 에러가남
// 첫번째 매개변수는 모든 종류의 객체가 될 수 있고 두번째는 해당 객체에서 모든 유형의 키가 될 수 있다고 했기 때문임
extractAndConvert({},'name') // '"name"' 유형의 인수는 'never' 유형의 매개변수에 할당할 수 없습니다.(2345)


// 해결법: name key를 추가하면 됌
extractAndConvert({name:'Max'},'name')

// 이렇게 사용하는 이유는 실수를 방지하기위함임
// 가령 지금은 name이란 key를 추가해줘서 에러가안나지만


// 이렇게 'age'로 바꿔주면 에러가남
extractAndConvert({name:'Max'},'age')
```

- 혹은 이렇게도 적용 가능

```js
// 제네릭을 선언할 때 <O extends keyof T> 부분에서 첫 번째 인자로 받는 객체에 없는 속성들은 접근할 수 없게끔 제한함
function getProperty<T, O extends keyof T>(obj: T, key: O) {
  return obj[key];
}
let obj = { a: 1, b: 2, c: 3 };

getProperty(obj, "a"); // okay
getProperty(obj, "z"); // error: "z"는 "a", "b", "c" 속성에 해당하지 않습니다.

```
