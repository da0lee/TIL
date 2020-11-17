> 소스코드 : prgrms-devjs3-practice

# Module

https://velog.io/@takeknowledge/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EB%AA%A8%EB%93%88-%ED%95%99%EC%8A%B5-%EB%82%B4%EC%9A%A9-%EC%9A%94%EC%95%BD-lwk4drjnni

- export한 각각의 모듈은 독립된 Scope를 갖고 있기 때문에 import하지 않으면 사용할 수 없다.
- 일부 module 시스템에선 확장명을 생략할 수 있지만, 네이티브 자바스크립트에서는 확장명이 있어야 한다.

#### export default
- 한 파일에서 하나의 개체만 넘길 수 있기 때문에 이름없는 함수, 배열도 넘길 수 있다.
```js
export default fuction(temp) {
alert(`오늘 낮 최고기온은 ${temp} °C 입니다.`)
} 
```

<br/>

```js
export default ['봄','여름','가을','겨울']
```

<br/>

export default sayTemp() 와 동일
```js
function sayTemp(temp) {
  alert(`오늘 낮 최고기온은 ${temp} °C 입니다.`)

  export {sayTemp as default}
}
```

<br/>

```js
import { api as authApi } from './auth';
import { api as usersApi } from './users';
import { api as postsApi } from './posts';

const apis = { authApi, usersApi, postsApi };

export default apis;
```