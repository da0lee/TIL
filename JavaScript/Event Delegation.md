# Event Delegation (이벤트 위임)

https://ko.javascript.info/event-delegation

- 많은 핸들러를 할당하지 않아도 되기 때문에 초기화가 단순해지고 메모리가 절약된다.
- 요소를 추가하거나 제거할 때 해당 요소에 할당된 핸들러를 추가하거나 제거할 필요가 없기 때문에 코드가 짧아진다.

```js
  this.$recentKeywordUl.addEventListener('click', (e) => {
    e.stopImmediatePropagation();
    if (e.target?.target.nodeName !== 'A') {
      this.onSearch(e.target.innerHTML);
      this.page = 1;
    }
  });
```