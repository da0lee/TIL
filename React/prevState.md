# prevState

1. 상태 값을 명시적 값으로 설정할 때

```js
this.setState({
  active: false,
});
```

<br/>

2. 
- 이전 상태를 기반으로 상태를 업데이트해야하는 경우 이 상태가 오래되었을 수 있으므로 this.state에서 직접 읽는 대신 함수를 사용해야 한다.

- 이전 값에 의존하는 방식으로 상태 값을 설정할 때 사용한다 (예 : 부울 토글, 숫자 증가).

```js
this.setState((prevState) => ({
  quantity: prevState.quantity + 1,
}));
```

