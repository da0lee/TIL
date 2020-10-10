> 소스코드: 1week-prgrms-rct-5-class-1_reviewer

> pages > Home > Post.js

<br/>

depth가 깊게 들어갈 때 1번처럼만 정의 가능한 줄 알았는데, 2번 처럼도 가능하다!

### 1번

```js
const { writer } = post;
const { name } = writer;
```

<br/>
### 2번

```js
const {
  writer: { name },
} = post;
```