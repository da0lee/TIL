# 기본 Type

> 2.3강 : 기본 타입 정리 1 (자바스크립트 간단 복습)

```jsx
{
  // JavaScript

  // let
  let name = 'dayoung';
  name = 'lee';

  // const
  const age = 20;
  // age = 5;
}
```

<br/>

> 2.4강 : 기본타입 정리 2 (number, string, boolean, undefined, null)

```jsx
{
  // Primitive : numbr, string, bloolean, bigint, symbol, null, undefined
  // Object : function, array...

  // number
  const num: number = -0.5;

  // string
  const str: string = 'hello';

  // boolean
  const bool: boolean = true;

  // undefined : 값이 있는지 없는지 결정되지 않은 상태
  // optional type일 때 사용. 단독적으로 undefined type을 지정하지는 않는다.
  // data type 이 있거나, 아직 결정되지 않았을 때(없을 때)는 보편적으로 undefined 를 사용한다.
  let name: string | undefined;
  name = undefined;

  // null : 값이 없음이 결정된 상태
  // 값이 없음을 나타낼 때는 null을 쓴다.
  let age: number | null;
  age = null;
}
```

<br/>

> 2.5강 : 기본 타입 정리 3 (unknown, any, void, never, object)

```jsx
{
  // unknown : 어떤 type이든 지정될 수 있어 가급적 사용하지 않는다.
  // ts는 type이 없는 js와 연동해서 쓸 수 있기 때문에 unknown type이 존재한다. ts에서 js library 를 이용하는 경우에 js에서 return하는 type을 모를 수가 있으므로 그럴 때 unknown을 사용한다.
  let notSure: unknown = 0;
  notSure = 'hi';
  notSure = true;

  //any : 되도록 사용하지 않는다.
  let anything: any = 0;
  anything = 'hello';

  // void : 함수에서 아무것도 return하지 않는다. type 설정 생략 가능. 변수에서는 잘 사용하지 않는다.
  function sayHello(): void {
    console.log('hello');
  }

  // never
  // 절대 return되지 않는 경우 그것을 명시하기 위해 쓰인다.

  function throwErr(message: string): never {
    // message -> server (log)
    // error를 던지고 함수가 죽게 된다. -> 함수가 return하는 값이 없다. -> return값이 없음을 never로 명시
    throw new Error(message);
  }

  function neverEnding(): never {
    // while문을 true로 지정해서 함수가 영원히 끝나지 않는 경우
    while (true) {}
  }

  // object : primitive가 아닌 모든 object들을 할당할 수 있다. 추상적이고 광범위하므로 사용을 지양한다.
  let obj: object;
  function acceptSomeObject(obj: object) {}

  acceptSomeObject({ name: 'dayoung' });
  acceptSomeObject({ age: 5 });
}
```

<br/>
<hr/>
<br/>

`오늘 공부한 것`

- https://academy.dream-coding.com/courses/take/typescript/lessons
