> 소스코드 : prgrms-devjs3-practice

<br/>

# 상세정보 API 요청


> App.js
```js

  ...

  this.searchResult = new SearchResult({
    $target,
    lastResult: this.lastResult,
    initialData: this.data,
    // 처음 랜더링 할 때 부터 detail 정보가 필요한 것은 아니기 때문에 App이 아닌 ImageInfo component에서 api 요청을 한다.
    onClick: (cat) => {
      // 요청했을 때 바로 setState로 가는 것이 아니라 showDetail을 거쳐 전달
      // click event 일어나면 visible을 true로 바꾸고, click한 cat(Item)의 정보 catData에 할당
      this.imageInfo.catDetails({
        visible: true,
        catData: cat,
      });
    },
  });

  this.imageInfo = new ImageInfo({
    $target,
    data: {
      visible: false,
      catData: null,
    },
  });

  ...

```

<br/>

> ImageInfo.js

```js
class ImageInfo {
  $imageInfo = null;
  data = null;

  constructor({ $target, data }) {
    const $imageInfo = document.createElement('div');
    $imageInfo.className = 'ImageInfo';
    this.$imageInfo = $imageInfo;
    $target.appendChild($imageInfo);

    this.data = data;
    this.render();
  }

  setState(nextData) {
    this.data = nextData;
    this.render();
  }

  catDetails(datas) {
    api.fetchCatDetail(datas.catData.id).then(({ data }) => {
      this.setState({
        visible: true,
        catData: data,
      });
    });
  }
  
  // 중복 코드 분리
  imageInfoDisplayNone() {
    this.$imageInfo.style.display = 'none';
  }

  // close btn 로직이 길어져 따로 분리.
  closeImageInfo() {
    this.$imageInfo.addEventListener('click', (e) => {
      if (e.target.className === 'close' || e.target.className === 'ImageInfo') {
        this.imageInfoDisplayNone();
      }
    });

    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') {
        this.imageInfoDisplayNone();
      }
    });
  }

  render() {
    if (this.data.visible) {
      const { name, url, temperament, origin } = this.data.catData;

      this.$imageInfo.innerHTML = `
        <div class="content-wrapper">
          <head class="title">
            <h2>${name}</h2>
            <button type="button" class="close">x</button>
          </head>
          <div class="img-container">       
            <img src="${url}" alt="${name}"/>
          </div>
          <div class="description">
            <p>성격: ${temperament}</p>
            <p>태생: ${origin}</p>
          </div>
        </div>`;
      this.$imageInfo.style.display = 'block';
      // 실행만
      this.closeImageInfo();
    } else {
      this.$imageInfo.style.display = 'none';
    }
  }
}

```

<br/>

> api.js

```js
const API_ENDPOINT = 'http://localhost:4001';

const api = {
  
  ...

  fetchCatDetail: (id) => {
    return fetch(`${API_ENDPOINT}/api/cats/${id}`).then((res) => res.json());
  },
};

```