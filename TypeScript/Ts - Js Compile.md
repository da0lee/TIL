# Ts -> Js Compile

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

https://nomadcoders.co/typescript-for-beginners/lectures/1650
