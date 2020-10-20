# Closer

내가 실행될 때의 환경을 기억하되 내가 사용하는 변수만 기억하고 있다. 예를 들어 내가 실행되는 환경의 부모함수에 변수 a,b가 있었지만 나는 변수 a만 이용한다면 closer에는 a만 저장되어있다.

### 1.
```js
// 문제 : i에 3이 찍힌다.
// 왜냐하면 for문은 0,1,2,3까지 돌기 때문이다. 다만 i < 3이라는 조건식에 따라 0,1,2번 까지만 data[i]에 들어갈 뿐이다. for문을 다 돌고 나면 i는 최종적으로 3이 된다.

var data = []

for (var i = 0; i < 3; i++) {
  data[i] = function() {
    console.log(i);
  }
}

// 해결 : 즉시 실행함수 안에서 리턴되는 값으로 내가 진짜 원하는 로직의 함수를 넣는다.

var data = []

for (var i = 0; i < 3; i++) {
  data[i] = (function(i) {
    return function() {
  console.log(i);
    }
  })(i)
}

data[0]()
data[1]()
data[2]()
```

<br/>

### 2.
```js
function foo() {
  const a = 10;
  const b = 20;
  function bar() {
    debugger;
    const sum = a + a;
		console.log(a)
  }
  return bar;
}
const bar = foo();
bar()

// 콜스택 
callStack = {
	1 : { //foo
		AO : {
			a: 10,
			b: 20,
			bar: function() {
				[[call]]:'const sum = a + a;'
			}
		},
		Scope : [AO, VO], 
		this: ''
	},
	0 : { // global
		VO : {
			bar: function() {
				[[call]]:'const sum = a + a;'
			}
			foo: function(){
				[[call]]: '....'
			}
		},
		Scope : [VO], 
		this: callStack.0.VO 
	}
}

```

<br/>

### 3.
```js
// 문제
let num = 0;
const 증가 = function() {
    return num++;
}

console.log(증가()); // 0
console.log(증가()); // 0
console.log(증가()); // 0

// 해결
const 증가 = (function(){
  let num = 0;
  return function () {
    return num++;
  }
})()
  
console.log(증가()); // 1
console.log(증가()); // 2
console.log(증가()); // 3

```

<br/>

### 4. 탭 메뉴

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
  </style>
</head>
<body>
    <ul class="buttons">
      <li>학교</li>
      <li>집</li>
      <li>공원</li>
    </ul>
    <div class="targets">
      <div>학교에서 놀았습니다.</div>
      <div>집에서 놀았습니다.</div>
      <div>공원에서 놀았습니다.</div>
    </div>
<script>
const buttons = document.querySelectorAll('.buttons > li');
const targets = document.querySelectorAll('.targets > div')

for (var i = 0; i < buttons.length; i++) {
  buttons[i].onclick = (function(j){ // 포문돌때 실행
    return function 알짜() { // 클릭될때 실행
      console.log(j);
      targets[j].style.backgroundColor = 'lime';
    }
  })(i)
}
```