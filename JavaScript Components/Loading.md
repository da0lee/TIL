> 소스코드 : prgrms-devjs3-practice

> Loading.js

<br/>

```js
class Loading {
  $loading = null;
  data = null;

  constructor({ $target }) {
    const $loading = document.createElement('div');
    this.$loading = $loading;

    $loading.className = 'Loading';
    $target.appendChild($loading);

    this.data = {
      show: false,
    };

    this.render();
  }

  show() {
    // setState를 실행시켜 this.data를 nextData로 바꾼다.
    // this.data = show / nextData = true
    this.setState({ show: true });
  }

  hide() {
    this.setState({ show: false });
  }

  setState(nextData) {
    // state 변경 후 
    this.data = nextData;
    // render안의 내용 실행 시킨다
    // render함수 호출을 안하면 state 변경만 하고 아무런 UI적 변화가 일어나지 않는다.
    this.render();
  }

  render() {
    if (this.data.show) {
      this.$loading.innerHTML = `
      <p>😺 고양이 소환 중 😺</p>
      `;
    } else {
      this.$loading.innerHTML = '';
    }
  }
}
```

<br/>

> App.js
```js
this.loading = new Loading({
  $target
})

this.searchInput = new SearchInput({
  $target,
  onSearch: (keyword) => {
    // loading Component를 보여줄 '시점 잡기'
    // api 요청 전 loading show
    this.loading.show();

    api.fetchCats(keyword).then(({ data }) => {
      // api 요청하고 data 넘어오면 loading hide
      this.setState(data);
      this.loading.hide();
    });
  },
});
```