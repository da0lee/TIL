# 💻 SearchActions

## 📂 카카오 지도 API에 검색 요청

<br/>

> src > redux > actions > SearchActions.js

<br/>

- Q ) 카카오 지도 API에 검색 요청
- A )  

```js
const getSearch = (mapElem) => async (dispatch, getState) => {
  try {
    let page = getState().search.page;
    let query = queryString.parse(history.location.search);
    let data = await apis.searchApi.getSearch({ ...query, page: page + 1 });

    // mapElem : map을 그려줄 div elem, query : 검색한 장소
    let map = mapElem ? initMap(mapElem, query) : getState().search.map;

    let result = [];
    result = data.map((store) => {
      let { _latitude, _longitude } = store.coordinates;
      let { imageNormal, imageOver } = makeMarkerImg(store.info.category);
      let point = new window.kakao.maps.LatLng(_latitude, _longitude);
      let marker = makeMarker(point, imageNormal);
      let infoWindow = makeInfoWindow(store);
      let mapData = { point, marker, imageNormal, imageOver, infoWindow };

      drawMap(map, mapData);

      return { ...store, mapData };
    });
    dispatch({
      type: SEARCH_INIT_DATA,
      payload: { data: result, map },
    });
  } catch (err) {
    console.log(err);
    console.log(err.response);
  }
};
```
