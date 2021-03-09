# Generator

1. 임의로 실행을 정지했다가 다시 실행시킬 수 있는 함수.     
정지하며 함수 내부에서 값을 빼오고, 다시 실행시키며 함수에 인자로 값을 넘길 수 있다.    
generator 함수 실행 중 다른 작업을 실행하다 다시 돌아와 next() 메서드를 실행하면 진행이 멈췄던 부분 부터 다시 실행할 수 있다.

2. next(), return(), throw() 속성을 가진다.
- next() : generator 함수 실행
- return() : 호출 즉시 done 속성값이 true 가 된다. 이후에 next()를 실행해도 value 를 얻어올 수 없다.
- throw() : return() 과 마찬가지로 done 속성이 true가 된다.

3. Iterator이면서 Iterable 하다. (반복 가능하다.)

- Iterable
    - Iterator를 반환하는 Symbol.iterator 메서드를 가진다.
    - for of 반복문, 구조 분해 할당(...)을 통해 개별 item 값을 가져올 수 있다.


- Iterator
    - 데이터 객체( {value: '', done: false} )를 반환하는 next 메서드를 가진다.
    - 작업이 끝나면 done이 true가 된다.

<br/>

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

## 메모리의 절약

<br/>

### 배열을 뒤집어 출력 시

### Reverse
```js
let arr = [1,2,3,4,5]

for (let value of arr.reverse) {
  console.log(value)
}
```
reverse 메서드로 인해 뒤집힌 배열이 하나 더 생성되어 메모리를 두 배로 사용하게 되었다.

<br/>

### Generator
```js
let arr = [1,2,3,4,5]

function * reverse(arr) {
  for (let i = arr.length-1; i >= 0; i--) {
    yield arr[i]
  }
}

for (let value of reverse(arr) {
  console.log(value)
})
```

<br/>

### Filter 기능 사용 시

### Filter
```js
let arr = [1,2,3,4,5]

for (let value of arr.filter((num)=> num >2)) {
  console.log(value)
}
```
filter 메서드로 인해 뒤집힌 배열이 하나 더 생성되어 메모리를 두 배로 사용하게 되었다.

<br/>

### Generator
```js
let arr = [1,2,3,4,5]

function * filter(arr, condition) {
  for (let value of arr) {
    if (condition(value){
      yield value
    })
  }
}

for (let value of reverse(arr, (num)=> num > 2) {
  console.log(value)
})
```


<br/>
<hr/>
<br/>

`오늘 공부한 내용`

- https://youtu.be/qi24UqyJLgs
- https://www.youtube.com/watch?v=qi24UqyJLgs
- https://youtu.be/VHS7V5Wkmyk
- https://youtu.be/WusTq2xa-C8