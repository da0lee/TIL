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

> 2.6 함수에서 타입 이용하기 (JS 💩 → TS ✨)

```jsx
{
  // 1
  // JS 💩
  function jsAdd(num1, num2) {
    return num1 + num2;
  }

  // TS ✨
  function tsAdd(num1: number, num2: number): number {
    return num1 + num2;
  }

  // 2
  // JS 💩
  function jsFetchNum(id) {
    // code ...
    return new Promise((resolve, reject) => {
      resolve(100);
    });
  }

  // TS ✨
  function tsFetchNum(id: string): Promise<number> {
    // code ...
    return new Promise((resolve, reject) => {
      resolve(100);
    });
  }
}
```

<br/>

> 2.7 함수 타입 이용 (spread, default, optional)

```jsx
// Optional Parameter : ?
{
  function printName(firstName: string, lastName?: string) {
    console.log(firstName);
    console.log(lastName);
  }
  printName('dayoung', 'lee');
  printName('ellie');
  printName('anna', undefined);

  // Default Parameter
  function printMessage(message: string = 'hello') {
    console.log(message);
  }

  printMessage();

  // Rest Parameter
  function addNumbers(...numbers: number[]): number {
    return numbers.reduce((a, b) => a + b, 0);
  }

  console.log(addNumbers(1, 2));
}
```

<br/>

> 2.8 배열과 튜플, 언제 튜플을 사용해야 할까?

```jsx
{
  // Array
  const fruits: string[] = ['🍒', '🍑', '🍉'];
  const scores: Array<number> = [1, 2, 3];

  // readonly: Object의 불변성 보존. 값을 읽을 수만 있고 변경할 수 없다.
  // readonly string[] 형식만 허용. Array<string> 형식은 아직 비허용
  function printArr(fruits: readonly string[]) {
    // 'readonly string[]' 형식에 'push' 속성이 없습니다.
    // fruits.push
  }

  // Tuple
  // 서로 다른type의 data를 함께 담을 수 있는 array.
  // 그러나 student[0],  student[1] 이런식으로 데이터를 찾는 것은 가독성이 굉장히 떨어진다. student.name, student.age 와 같은 형식으로 명시할 수 있게, 되도록 interface, type alias, class 등으로 대체해서 사용.
  // 값을 동적으로 return하는데, interface, type alias, class로 묶기 애매하고, 관련 있는 다른 type의 data를 묶ㅇ서 사용자가 이름을 정의해서 쓸 경우 유용.

  // 1
  // ASIS
  let student: [string, number];
  student = ['dayoung', 20];
  student[0]; // 'dayoung'
  student[1]; // 20

  // TOBE : 구조분해 할당으로 가독성 개선. 그러나 이 방법도 데이터가 정해지는 곳이 아니라 사용하는 곳에서 이름을 결정하고 쓴다는 단점이 있다.
  const [name, age] = student;

  // 2 : React의 useState
  // const [count, setCount] = useState(0);
  // useState : return type을 tuple을 이용해 정의. 초기데이터값 S, 값을 업데이트할 수 있는 API Dispatch<SetStateActions<S>> 반환.
  // [S, Dispatch<SetStateActions<S>>]
}
```

<br/>

> 2.9 타입스크립트의 꽃 🌷 Type Alias

```jsx
{
  // Type Aliases (별명)

  // 1
  type Text = string;
  const name: Text = 'dayoung';

  type Student = {
    name: string,
    class: number,
  };
  const student: Student = {
    // age : 9 //err
  };

  // 2 : String Literal Types : 문자열 외에도 Boolean등 다양한 type 지정 가능
  type JSON = 'json';
  let json: JSON = 'json';

  type Boal = true;
  const isCat: Boal = true;
}
```

<br/>

> 2.10 진정한 타입스크립트의 시작! Union 타입

```jsx
{
  //  Unon Types: OR
  // 발생할 수 있는 모든 case 중 하나만 할당할 수 있을 때 사용
  type Direction = 'left' | 'rignt' | 'up' | 'down';
  function move(direction: Direction) {
    console.log(direction);
  }

  move('left');

  // String Literal Types 사용 시에도 동일한 결과를 얻을 수 있다.
  type TileSize = 8 | 16 | 32;
  const tile: TileSize = 1;
  // '1' 형식은 'TileSize' 형식에 할당할 수 없습니다.
  const tile2: TileSize = 8;

  // 예제
  // 성공할 수도, 실패할 수도 있는 login이란 함수가 있을 때 성공할 경우, network에서 받아온 response를 return하고, 실패할 경우 실패한 이유를 알려줄 때 union을 사용한다.

  type SuccessState = {
    response: {
      body: string,
    },
  };
  type FailState = {
    reson: string,
  };
  type LoginState = SuccessState | FailState;
  function login2(id: string, pw: string): Promise<LoginState> {
    return;
  }
}
```

<br/>

> 2.11 필수 타입! Discriminated Union 🚀

```jsx
{
  // printLoginState(state)
  // success -> response.body 출력, faile -> reson 출력
  function printLoginState(state: LoginState) {
    if ('response' in state) {
      console.log(`${state.response.body}`);
    } else {
      console.log(`${state.reson}`);
    }
  }
}
```

<br/>
<hr/>
<br/>

`오늘 공부한 것`

- https://academy.dream-coding.com/courses/take/typescript/lessons
