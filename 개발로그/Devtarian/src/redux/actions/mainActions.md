# 💻 MainActions

## 📂1 Slider next Btn 클릭시 data 추가 요청

<br/>

> src > redux > actions > mainActions.js

<br/>

- Q ) Slider next Btn 클릭시 data 추가 요청
- A )  

```js
const fetchMore = (query) => async (dispatch, getState) => {
  try {
    //  getState() : 
    // - 현재 state를 가져온다.
    // - useState()의 setState를 함수형으로 업데이트 하는 것과 비슷. 바뀐 prevState를 받아와 그 값을 update 한다.
    const page = getState().main[query.type].page;
    const data = await apis.mainApi.fetchMore({ ...query, page: page + 1 });

    dispatch({
      type: MAIN_FETCH_MORE,
      payload: { type: query.type, data },
    });
  } catch (err) {
    console.log(err);
    console.log(err.response ? err.response : err);
  }
};
```
