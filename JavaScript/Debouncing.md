# Debouncing

- form 입력이나 페이지 스크롤링 등 짧은 시간 안에 빈번하게 발생되는 브라우저 이벤트들이 있다. 디바운싱은 위 같은 이벤트를 다룰 때, 실제로 함수가 다시 호출되기 전까지 시간 간격을 두어 성능 이슈를 해결하는 방법 중의 하나다.

- 설정 시간 전에 이벤트를 호출하면 setTimeout을 계속 clear하기 때문에 실행 구문이 실행되지 않는다. 검색어 추천이나 중복ID 체크처럼 form 입력 시, 1,2초 정도의 디바운싱만 적용 해도 입력되는 자음, 모음 마다가 아닌 완성된 타이핑으로 서버에 요청을 보내도록 만들 수 있다.


<br/>

### Debounce를 적용한 검색어 추천

```js
const [state, setState] = useState({
  address: '서울 강남구 강남역',
  lat: 33.450701,
  lng: 126.570667,
  region: '',
  keyword: '',
  map: '',
  marker: '',
  recommends: [],
  isSearching: false,
});

const { lat, lng, keyword, map, marker, recommends, isSearching } = state;
const eventSearchKeyword = useCallback(() => {
  var geocoder = new window.kakao.maps.services.Geocoder();
  geocoder.addressSearch(keyword, function (data, status) {
    if (status === window.kakao.maps.services.Status.OK) {
      setState((state) => ({
        ...state,
        recommends: data.slice(0, 4),
        lat: data[0].y,
        lng: data[0].x,
      }));
    }
  });
}, [keyword]);

useEffect(() => {
  if (!isSearching) return;
  const timeDelaySearch = setTimeout(() => {
    eventSearchKeyword();
  }, 1000);
  return () => clearTimeout(timeDelaySearch);
}, [isSearching, eventSearchKeyword]);

const handleChange = (e) => {
  setState((state) => ({
    ...state,
    keyword: e.target.value,
    isSearching: true,
  }));
};
```

<br/>
<hr/>
<br/>

### 참고

- https://joshua1988.github.io/web-development/javascript/javascript-interview-3questions/
- https://bityoungjae.com/2019/11/09/JavaScript/%EA%B0%9C%EB%85%90%EC%A0%95%EB%A6%AC/%EB%94%94%EB%B0%94%EC%9A%B4%EC%8B%B1%EA%B3%BC%20%EC%93%B0%EB%A1%9C%ED%8B%80%EB%A7%81/
- https://jm-web.tistory.com/33
- https://sub0709.tistory.com/52