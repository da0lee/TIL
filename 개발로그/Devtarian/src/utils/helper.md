# 💻 Helper

## 📂1 영업시간 선택 (selectInput)

<br/>

> src > utils > helper.js

<br/>

- Q ) 영업시간 선택 (selectInput)
- A ) 

```js
// 1.시작시간 (startTime)이 들어온다. (ex. 07시 00분)
export const timeSelect = (startTime) => {
  const result = [];

  // 2. 선택된 시작시간(ex. 07시 00분)이 있으면 07을 startTimeidx로 정한다.
  const startTimeidx = startTime ? startTime.split('시')[0] : 0;
  // 3. 반복문을 돌며 startTimeidx 와 같거나 큰 select option들만 변수 result에 담는다. 
  for (let i = 0; i <= 24; i++) {
    if (i >= startTimeidx) {
      result.push(`${i}시 00분`);
    }
  }
  return result;
};
```
