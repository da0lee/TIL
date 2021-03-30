# Ts -> Js Compile

interface 는 js로 compile 되지 않는다. 그러므로 interface 를 js 로 넣고 싶은 경우가 생기면, interface 대신 class 를 쓰면 된다.

```
interface

- interface 에 선언된 property, method의 구현을 강제하여 일관성을 유지할 수 있도록 한다. 일반적으로 type 체크를 위해 사용되며 변수, 함수, class에 사용할 수 있다.

- property, method를 가질 수 있다는 점에서 class와 유사하나 직접 인스턴스를 생성할 수 없고 모든 method는 추상 method다.

- ES6는 interface를 지원하지 않지만 TypeScript는 지원한다.
```

<br/>

### TS

```js
class Human {
  public name: string;
  private age: number;
  public gender: string;
  constructor(name: string, age: number, gender: string) {
    this.name = name;
    this.age = age;
    this.gender = gender;
    // 이 class의 gender는 생성자의 gender와 같다는 뜻
  }
}

const dayoung = new Human('dayoung', 20, 'female');

const sayHi = (person: Human): string => {
  return `Hello ${person.name}, you are ${person.age}, you are a ${person.gender}!`;
  // error : 'age' 속성은 private이며 'Human' 클래스 내에서만 액세스할 수 있습니다.
};

console.log(sayHi(dayoung));

export {};

```

<br>

### JS

```js
'use strict';
Object.defineProperty(exports, '__esModule', { value: true });
class Human {
  constructor(name, age, gender) {
    this.name = name;
    this.age = age;
    this.gender = gender;
    // 이 class의 gender는 생성자의 gender과 같다는 뜻
  }
}
const dayoung = new Human('dayoung', 20, 'female');
const sayHi = (person) => {
  return `Hello ${person.name}, you are ${person.age}, you are a ${person.gender}!`;
  // error : 'age' 속성은 private이며 'Human' 클래스 내에서만 액세스할 수 있습니다.
};
console.log(sayHi(dayoung));
//# sourceMappingURL=index.js.map
```

<br>

`오늘 공부한 것`

- https://nomadcoders.co/typescript-for-beginners/lectures/1650
- https://poiemaweb.com/typescript-interface
