> 소스코드 : prgrms-devjs3-practice

<br/>

# Infinity Scroll

> SearchResult.js
```js
class SearchResult {
  $wrap = null;
  $searchResult = null;
  data = null;
  keyword = null;
  lastResult = null;
  onClick = null;
  onNextPage = null;

  constructor({ $target, lastResult, initialData, keyword, onClick, onNextPage }) {
    const $wrap = document.createElement('section');
    const $searchResult = document.createElement('ul');
    this.$searchResult = $searchResult;

    this.$searchResult.className = 'SearchResult';
    $target.appendChild($wrap);
    $wrap.appendChild($searchResult);

    this.data = initialData;
    this.keyword = keyword;
    this.lastResult = lastResult;
    this.onClick = onClick;
    this.onNextPage = onNextPage;
    this.render();
  }

  setKeyword(nextKeyword) {
    this.keyword = nextKeyword;
  }

  setState(nextData) {
    this.data = nextData;
    this.lastResult = nextData;
    this.render();
  }

  // items : 객체 목록, observer : 관찰자 parameter로 전달
  listObserver = new IntersectionObserver((items, observer) => {
    items.forEach((item) => {
      // isIntersectiong: 타겟 요소가 현재 교차 루트와 교차하는지 여부를 boolean 값으로 알려줌.
      // 아이템이 화면에 보일 때
      if (item.isIntersecting) {
        // Lazy loading : 레이기존에 placeholder로 차지하고 있던 공간에 진짜 img src 대입
          // 이미지를 로드
        item.target.querySelector('img').src = item.target.querySelector('img').dataset.src;
      
        // 마지막 요소를 찾아내고
        let dataIndex = Number(item.target.dataset.index);
        // 마지막 요소라면 onNextPage 호출
        if (dataIndex=== this.data.length -1) {
          this.onNextPage();
        }
      }
    });
  });

  render() {
    if (this.keyword == null && (this.lastResult == null || this.lastResult.length == 0)) {
      return;
    }

    if (this.data?.length > 0) {
      this.$searchResult.innerHTML = this.data
        .map(
          (cat, index) => `
        <li class="item" data-index=${index}>
          <img src='https://via.placeholder.com/200x300' data-src=${cat.url} alt=${cat.name} />
        </li>
      `
        )
        .join('');
    } else {
      this.$searchResult.innerHTML = `
      <div class="noItem">
        <p>🐈<br/>요청하신 고양이를<br/>찾을 수 없습니다.</p>
      </div>`;
    }

    this.$searchResult.querySelectorAll('.item').forEach(($item, index) => {
      $item.addEventListener('click', () => {
        this.onClick(this.data[index]);
      });
      // Observer 등록
      // observe method의 인자에 target 요소를 넣어 관찰 시작
      this.listObserver.observe($item);
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
  lastResult = null;
  // page 정의
  page = 1;

  ... 

  this.searchResult = new SearchResult({
    $target,
    lastResult: this.lastResult,
    initialData: this.data,
    onClick: (cat) => {
      this.imageInfo.catDetails({
        visible: true,
        catData: cat,
      });
    },
    onNextPage: () => {
      // 전달할 검색어
      const recentKeywords = localStorage.getItem('recentKeywords')
        ? localStorage.getItem('recentKeywords').split(',')
        : [];
      // 전달할 page 
      const page = this.page + 1;
      this.loading.showLoading();
      api.fetchNextCats(recentKeywords, page).then(({ data }) => {
        // newData : 넘어온 새로운 data를 기존 data 뒤에 붙혀주었다.
        let newData = this.data.concat(data);
        this.loading.hideLoading();
        // setState에서 검색결과를 뿌려주는 searchResult component에 뿌려줄 data값을 관리하고 있으므로 concat한 data를 setState에 전달해준다.
        this.setState(newData);
        // const page = this.page + 1; 까지만 하면 page가 1 +1 = 2에서 변하지 않으므로 더한 값 this.page에 재 할당 
        this.page = page;
      });
    },
  });

  setState(nextData) {
    console.log(this);
    this.data = nextData;
    this.searchResult.setState(nextData);
  }

  ...

}

```

<br/>

> api.js
```js
const API_ENDPOINT = 'http://localhost:4001';

const api = {

  ... 

  fetchNextCats: (keyword, page) => {
    return fetch(`${API_ENDPOINT}/api/cats/search?q=${keyword}&page=${page}`).then((res) => res.json());
  },

  ...

};

```