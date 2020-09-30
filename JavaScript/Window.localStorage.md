> 소스폴더: kinfork

> Pages > MyAccout > MyAccount.js
 
  <br/>

# Window.localStorage

https://developer.mozilla.org/ko/docs/Web/API/Window/localStorage

<br/>

*  localStorage 읽기 전용 속성을 사용하면 Document 출처의 Storage 객체에 접근할 수 있다. 
* 저장한 데이터는 브라우저 세션 간에 공유된다. 
* localStorage는 sessionStorage와 비슷하지만, localStorage의 데이터는 만료되지 않고 sessionStorage의 데이터는 페이지 세션이 끝날 때, 즉 페이지를 닫을 때 사라지는 점이 다르다.     
 ("사생활 보호 모드" 중 생성한 localStorage 데이터는 마지막 "사생활 보호" 탭이 닫힐 때 지워진다.)


* localStorage에 저장한 자료는 페이지 프로토콜별로 구분힌다.     
특히 HTTP(http://example.com)로 방문한 페이지에서 저장한 데이터는 같은 페이지의 HTTPS(https://example.com)와는 다른 localStorage에 저장된다.

* 키와 값은 항상 각 문자에 2바이트를 할당하는 UTF-16 DOMString의 형태로 저장합니다. 객체와 마찬가지로 정수 키는 자동으로 문자열로 변환한다.

<br/>

###  Storage.setItem()

<br/>

현재 도메인의 로컬 Storage 객체에 접근한 후, 항목 하나를 추가

```js
localStorage.setItem('myCat', 'Tom');
```

<br/>

### Storage.getItem()

<br/>

추가한 localStorage 항목을 읽을 때

```js
const cat = localStorage.getItem('myCat');
```

<br/>

### Storage.removeItem()

<br/>

제거

```js
localStorage.removeItem('myCat')
```
<br/>

### Storage.clear();

<br/>

localStorage 항목의 전체 제거

```js
localStorage.clear();
```
<br/>

```js
// logout 할 때 login 정보 null로 설정
  Logout = () => {
    this.setState({ access: false });
    localStorage.setItem("login", JSON.stringify(null));
  };

  componentDidMount() {
    const { id } = this.props.match.params;
    let temp;

    // localStorage에 login 정보가 없으면 temp = null, 있으면 login에 저장된 정보 읽어온 값으로 설정
    localStorage.getItem("login") === "undefined"
      ? (temp = null)
      : (temp = JSON.parse(localStorage.getItem("login")));

    temp !== null
      ? this.setState({ pageIdx: addressConfirmObj[id], access: true })
      : this.setState({ pageIdx: addressConfirmObj[id], access: false });
  }
```