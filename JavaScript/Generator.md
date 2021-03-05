# Generator

1. 함수의 실행을 멈췄다 재개할 수 있다.

2. next(), return(), throw() 속성을 가진다.
- next() : generator 함수 실행
- return() : 호출 즉시done 속성값이 true 가 된다. 이후에 next()를 실행해도 value 를 얻어올 수 없다.
- throw() : return() 과 마찬가지로 done 속성이 true가 된다.

```js

function* fn () {
  // 함수를 쭉 실행하다 yeild를 만나면 데이터 객체( {value: '', done: false} )를 반환한다. 
  // value : yeild 오른쪽 값 (혹은 함수). 값을 생략하면 undefined
  // done : 함수 코드가 끝났는지 여부
  yeild 1   // {value: 1, done: false}
  yeild 2   // {value: 2, done: false}
  yeild 3   // {value: 3, done: false}
  return 4  // {value: 4, done: true}
} 

// generator 함수를 실행하면 return값이 아닌 generator 객체가 반환된다.
// fn {<suspended>}
const result = fn() 
```
<br/>
<hr/>
<br/>

### 참고

- https://youtu.be/qi24UqyJLgs