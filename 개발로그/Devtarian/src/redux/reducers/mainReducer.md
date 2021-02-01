# 💻 MainReducers

## 📂1 Slider next Btn 클릭시 data 추가 요청

<br/>

> src > redux > reducers > mainReducers.js

<br/>

- Q ) Slider next Btn 클릭시 data 추가 요청
- A ) 

```js
const INIT_STATE = {
  isFetching: true,
  // data: {},
  store: { data: [], page: 1, size: 1, fetchMore: true },
  rated: { data: [], page: 1, size: 1, fetchMore: true },
  wiki: { data: [], page: 1, size: 1, fetchMore: true },
  review: { data: [], page: 1, size: 1, fetchMore: true },
  // size : (= limit) 원래 4개씩 더 불러와서 next Btn 클릭시 불러 온 data 중 하나씩 더 보여주어야 하는데, 그럼 기존에 만든 carousel을 전면 개편해야해서 일단 일정에 맞추기 위해 1로 설정하였다.. 반성합니다.
  // fetchMore : data를 더 불러올수 있는지 여부로 사용. true : 더 불러올 수 있다. / false : 더 불러올 수 없다.
};

...

case MAIN_FETCH_MORE:
  const type = action.payload.type;
  return {
    ...state,
    [type]: {
      ...state[type],
      data: [...state[type].data, ...action.payload.data],
      page: state[type].page + 1,
      // 받아온 data길이가 설정한 size 보다 작으면 data를 요청하지 않는다.
      fetchMore: action.payload.data.length < state[type].size ? false : true,
    },
  };
```
