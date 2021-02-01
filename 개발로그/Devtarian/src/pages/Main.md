# 💻 Main

## 📂1-1 QueryString 객체 형태로 받기

<br/>

> src > pages > main > section > Section.js

<br/>

- Q ) QueryString 객체 형태로 받기
- A ) 
  - https://justmakeyourself.tistory.com/entry/querystring-path-of-react-router
  - 아래와 같이 queryString.parse() 를 해주면 아주 편리하게 객체형태의 쿼리스트링을 받을 수 있다!

```js
 const query = queryString.parse(history.location.search);
```
<br/>

### ASIS
```js
?lat=37.6031007&lng=127.02928809999999
```
### TOBE
```js
{lat: "37.6031007", lng: "127.02928809999999"}
```

<br/>

## 📂1-2 사용자의 위치 정보 요청

<br/>

> src > pages > main > section > Section.js

```js
useEffect(() => {
  // 사용자가 최초 접속했을 시에는 query에 lat, lng이 포함되어 있지 않다. 그래서 return 이후의 코드(사용자 현재 위치 정보 요청)가 실행되지만, 이미 위치 정보를 받아왔고 사용자가 '계속 허용'을 설정한 상태라면 return을 해 위치 정보 요청 코드가 재 실행되지 않도록 한다.
  if (lat || lng) return;
  window.navigator.geolocation.getCurrentPosition((pos) => {
    const { latitude, longitude } = pos.coords;
    window.location = `?lat=${latitude}&lng=${longitude}`;
  });
}, [lat, lng]);
```

