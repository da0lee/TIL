> 소스코드: 1week-prgrms-rct-5-class-1_reviewer

> hocs > toggle.js

<br/>

# HOC : toggle

https://velog.io/@hwang-eunji/React-%EA%B3%A0%EC%B0%A8-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-HOC-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0

https://velopert.com/3537

<br/>

HOC는

1. 리액트 컴포넌트를 파라미터로 받아서
2. 함수 내부에서 새 컴포넌트를 만든 다음
3. 해당 컴포넌트 안에서 파라미터로 받아온 컴포넌트를 렌더링 하여
4. 다른 리액트 컴포넌트를 반환하는 고차함수다.

함수를 통하여 컴포넌트에 우리가 준비한 특정 기능을 부여하고 싶을 때 쓰인다. (주로 인증 체크)

```
[ 인증체크 ]

아무나 진입 가능한 페이지, 로그인 한 회원만 진입 가능한 페이지,로그인 한 회원은 진입하지 못하는 페이지, 관리자만 진입 가능한 페이지 등을 컨트롤.
```

ex) REDUX - connect() / ROUTER - withRouter()

<br/>

```js
import React from 'react';

function toggle(WrappedComponent) {
  return function ToggleWrapped(props) {
    return props.show ? <WrappedComponent {...props} /> : false;
  };
}

export default toggle;
```

```js
import toggle from '@/hocs/toggle';

export default toggle(NaviItem);
export default toggle(Profile);
```

여기서는 NaviItem, Profile 함수를 감싸주었다.