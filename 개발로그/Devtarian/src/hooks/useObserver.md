# 💻 useObserver (무한 스크롤링)

<br/>

> src > hooks > useObserver.js

<br/>

- Q ) Customed hook 으로 무한 스크롤링 구현하기
- A ) 

```js
import { useRef, useEffect, useCallback } from 'react';

const useObserver = (fetchApiData) => {
  const ref = useRef();

  // 관찰할 대상(Target)이 등록되거나 가시성(Visibility, 보이는지 보이지 않는지)에 변화가 생기면 관찰자는 콜백(Callback)을 실행한다.
  const handleObserver = useCallback(
    (entries, observer) => {
      entries.forEach((entry) => {
        if (!entry.isIntersecting) return;
        fetchApiData();
        observer.unobserve(entry.target);
      });
    },
    [fetchApiData]
  );

  useEffect(() => {
    // Observer(관찰자) 초기화
    const options = { threshold: 0.5 };
    const observer = new IntersectionObserver(handleObserver, options);

    // 설정해둔 ref에 도달하면 관찰 시작
    if (ref.current) {
      observer.observe(ref.current);
    }
    // 관찰해제
    return () => observer && observer.disconnect();
  }, [ref, handleObserver]);

  return ref;
};

export default useObserver;

```
