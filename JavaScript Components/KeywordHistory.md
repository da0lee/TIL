> 소스코드 : prgrms-devjs3-practice

<br/>

# 최근 검색어 저장

<br/>

> KeywordHistory

```js
class KeywordHistory {
  $keywordHistory = null;
  data = null;

  constructor({ $target, onSearch }) {
    const $keywordHistory = document.createElement('ul');
    this.$keywordHistory = $keywordHistory;
    this.$keywordHistory.className = 'KeywordHistory';
    this.onSearch = onSearch;

    $target.appendChild(this.$keywordHistory);

    // constructor안에서 data(state) 초기화, render
    this.init();
    this.render();
  }

  // 컴포넌트 실행될 때 data(state) 업데이트
  init() {
    const data = this.getHistory();
    this.setState(data);
  }

  // SearchInput에서 e.target.value를 인자(keyword)로 전달해 주었다.  
  addKeyword(keyword) {
    let keywordHistory = this.getHistory();
    keywordHistory.unshift(keyword);
    // 최근 검색결과가 5개 까지만 보이도록
    keywordHistory = keywordHistory.slice(0, 5);
    // localHistory에 keywordHistory저장. localHistory에는 string 형태만 저장이 되므로, 입력값을 ,로 join해준다. (join: 배열 내 요소들을 합쳐 string값으로 반환) 
    localStorage.setItem('keywordHistory', keywordHistory.join(','));
    // e.target.value 더한 값으로 다시 초기화(setState)
    this.init();
  }
  
  // localStorage의 keywordHistory 가져옴. 아직 값이 저장되기 전이면 배열(keywordHistory)에 붙힌 method 들에 err가 발생하므로 [] 빈 배열을 반환하게 처리해준다.
  getHistory() {
    return localStorage.getItem('keywordHistory') === null ? [] : localStorage.getItem('keywordHistory').split(',');
  }

  // state 변경하고, 바뀐 결과 rendering
  setState(nextData) {
    this.data = nextData;
    this.render();
  }

  render() {
    this.$keywordHistory.innerHTML = this.data
      .map(
        (keyword) => `
    <li><button>${keyword}</button></li>
    `
      )
      .join('');

    // 매 keyword들 마다 event감지기를 붙힌다. 
    // click시 해당 el을 SearchInput의 onSerach()에 전달. 
    this.$keywordHistory.querySelectorAll('li button').forEach(($item, index) => {
      $item.addEventListener('click', () => {
        this.onSearch(this.data[index]);
      });
    });
  }
}
```

<br/>

> SearchInput

```js
class SearchInput {
  keywords = [];

  constructor({ $target, onSearch }) {
    const $wrap = document.createElement('section');
    const $searchInput = document.createElement('input');
    this.$searchInput = $searchInput;
    this.$searchInput.placeholder = '고양이를 검색해보세요.|';

    $searchInput.className = 'SearchInput';
    $target.appendChild($wrap);
    $wrap.appendChild($searchInput);

    // 'keyup' event는 한글 입력 시 event가 두번씩 일어나 'keypress'로 변경
    $searchInput.addEventListener('keypress', (e) => {
      if (e.key === 'Enter') {
        onSearch(e.target.value);
        // 최근 키워드 저장
        this.KeywordHistory.addKeyword(e.target.value);
      }
    });
    // KeywordHistory component 불러옴
    this.KeywordHistory = new KeywordHistory({
      $target,
      onSearch,
    });
  }
}

```

<br/>

> App.js

```js
class App {
  $target = null;
  data = [];

  constructor($target) {
   
    ... 

    this.searchInput = new SearchInput({
      $target,
      onSearch: (keyword) => {
        this.loading.showLoading();
        api.fetchCats(keyword).then(({ data }) => {
          this.loading.hideLoading();
          this.setState(data);
          // 검색 이벤트 이후 localStorage에 [key: 'lastResult', value: 방금 검색어의 검색결과] 저장
          this.saveResult(data);
        });
      },
    });

    // app 실행 시 마지막 검색결과 노출
    this.init();
  }

  ...
  // server에서 result가 object 형태로 들어오고, localstorage에는 string 형태로만 저장이 되므로 JSON.stringify 
  saveResult(result) {
    localStorage.setItem('lastResult', JSON.stringify(result));
  }

  init() {
    const lastResult =
      // localStorage에 lastResult가 string 형태로 저장되어 있으므로 JSON.parse 하여 사용가능한 data type으로 변경해준다.
      localStorage.getItem('lastResult') === null ? [] : JSON.parse(localStorage.getItem('lastResult'));
    this.setState(lastResult);
  }
}
```