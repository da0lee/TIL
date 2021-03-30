# 1.1 TypeScript란?

![https://miro.medium.com/max/606/1*eurMn0omz2KIejNIV06Vsg.png](https://miro.medium.com/max/606/1*eurMn0omz2KIejNIV06Vsg.png)

출처: [https://morioh.com/p/68a5f1f5b6b9](https://morioh.com/p/68a5f1f5b6b9)

<br/>

# JS

- Dynamically typed : 프로그램이 동작할 때 실시간으로 type이 결정됨
- Runtime시 error 발생

```jsx
// runtime 때 변수의 type이 결정되기 때문에, 프로그래밍, compile 시에는 아직 type이
// 결정되어 있지 않아 다음 같은 예제가 가능하다.

let name = 'dayoung';
name = 10;
```

- Prototype base 언어 : Constructor Funtions 를 이용해 class 에서 처럼 Object 를 구현 할 수 있고, ES6 이후로 class가 도입되었지만, 강력한 객체지향 프로그래밍은 어렵다.

<br/>

# TS

- Statically typed : type 이 고정되어 있다.
- Compile 시 error 발생 : 코딩 시 즉각적으로 error를 받아볼 수 있다.

```jsx
// 한 번 결정된 type은 절대 바뀌지 않는다.
let name: string = 'dayoung';
name = 10; // error
```

- 강력한 객체지향 프로그래밍 가능 : 다른 class 기반 프로그래밍 언어처럼 class, interface, generic 활용.

<br/>
<hr/>
<br/>

`오늘 공부한 것`

- https://academy.dream-coding.com/courses/take/typescript/lessons
