> 소스코드: 이솝

> Pages > Product > Productdetails.js

<br/>

# 불러온 data에 ' , '붙혀 나열하기(마지막item 제외)

```js
{item.skin_types.map((el) => {
  // lastIndex : data 배열 전체중 마지막 index
  const lastIndex = item.skin_types.length - 1;
  // lastEl : 마지막 item
  const lastEl = item.skin_types[num];
  if (el === lastEl) {
    // 마지막 item이면 , 제외
    return `${el.name}`;
    // 불러온 item에 ,붙히기
  } else {
    return `${el.name}, `;
  }
})}
```