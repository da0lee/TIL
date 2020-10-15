> 소스코드 : 1week-prgrms-rct-5-class-1_Sky_working

> utils > postMockStore.js

<br/>

# Setter 

https://poiemaweb.com/es6-class     
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/set



### set 문법

{set prop(val) { ... } }

### 파라미터

prop : 프로퍼티를 가져올 함수 이름

setter는 클래스 필드에 값을 할당할 때마다 클래스 필드의 값을 조작하는 행위가 필요할 때 사용한다.
( = 프로퍼티 값이 변경되어 질 때마다 함수를 실행하는데 사용)

setter는 메소드 이름 앞에 set 키워드를 사용해 정의한다. 이때 메소드 이름은 클래스 필드 이름처럼 사용된다. 다시 말해 setter는 호출하는 것이 아니라 프로퍼티처럼 값을 할당하는 형식으로 사용하며 할당 시에 메소드가 호출된다.

```js
// localStorage에 data 요청하는 부분 import
import { getLocalStorageData } from './utils';

// key import
import { USER_POSTS_KEY } from './data';

export default class PostMockStore {
  // posts state 설정. 초기값은 빈 배열
  constructor() {
    this.posts = [];
  }
  

  // setPosts : 프로퍼티를 가져올 함수 이름
  set setPosts(newPosts) {
    try {
      // newPosts가 array 형태가 아니면 에러 던짐
      if (!Array.isArray(newPosts)) {
        throw new Error(`invalid Value`);
      }

      // newPosts가 array 형태가 맞으면 newPost 로 할당
      this.posts = newPosts;

      // err 가 발생하면 해당 err 표시
    } catch (err) {
      console.log(`Cannot set posts value..${err}`);
    }
  }
  // localStorage로부터 data 가져오는 로직
  getPostFromLS = () => {
    this.posts = getLocalStorageData(USER_POSTS_KEY);
    // 할당 후 this.posts; 반환
    return this.posts;
  };
}
```