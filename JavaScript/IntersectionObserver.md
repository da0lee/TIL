> 소스폴더: kinfork

# IntersectionObserver

https://heropy.blog/2019/10/27/intersection-observer/

  <br/>

### [ 개요 ]

  <br/>
  
  Intersection observer는 기본적으로 브라우저 뷰포트(Viewport)와 설정한 요소(Element)의 교차점을 관찰하며, 요소가 viewport에 포함되는지 포함되지 않는지, 더 쉽게는 사용자 화면에 지금 보이는 요소인지 아닌지를 구별하는 기능을 제공한다.

  root 옵션에는 가시성의 판단 기준이 될 HTML 엘리먼트를 지정. observe 메소드로 등록하는 엘리먼트들은 반드시 이 루트 엘리먼트의 자식이어야 한다. ( default는 브라우저 화면에서 현재 보이는 영역인 viewport ) 루트 엘리먼트를 지정하면 현재 화면과는 상관없이 루트 엘리먼트와 등록한 엘리먼트들의 영역이 교차하는 지 판단하게 된다.

  <br/>

### [ threshold ]

  <br/>

  관측 대상에 대한 전체 상자 영역(루트)에 대한 교차 영역의 비율을 지정하며, 0.0과 1.0 사이의 숫자 하나 혹은 숫자 배열. 0.0 값은 대상의 단일 픽셀이라도 보여지면, 대상이 보이는 것으로 계산되는 것을 의미한다. 1.0은 전체 대상 요소가 표시됨을 의미. ( default는 0.0 )
   
  
  <br/>


### [ return 값 ]
  <br/>
  지정된 가시성 threshold 를 통해 지정된 root 내에서 대상 요소의 가시성을 감시하는 데 사용할 수있는 IntersectionObserver 인스턴스가 반환됩니다. observe() 메소드를 호출하여 지정된 대상의 가시성 변경을 관찰하십시오.
 
  <br/>

### [ 예제 ]
  <br/>
  아래는 요소의 보여지는 부분이 10% 가 넘거나 작아질 때 myObserverCallback 를 호출하는 새로운 intersection observer 를 생성하는 예제.

```js
let observer = new IntersectionObserver(myObserverCallback, { threshold: 0.1 });
```

<br/>

```js
const useScrollLogo = () => {
  // <img> 에서 useScrollLogo 함수가 실행되므로 current는 img
  const dom = useRef();

  // 콜백은 2개의 인수(entries, observer)를 가진다.[entry]는 handleScroll가 가지는 인수
  const handleScroll = useCallback(([entry]) => {
    const { current } = dom;

    const scrollMatrix = () => {
      window.onscroll = () => {
        const pageYOffset = window.pageYOffset;
        let xSet = 5 - pageYOffset / 46;
        let ySet = 190 - pageYOffset * 1.03;

        current.style.transform = `matrix(${
          xSet <= 5 && xSet >= 1 ? xSet : 1
        },0,0,${xSet <= 5 && xSet >= 1 ? xSet : 1},0,${
          ySet >= 0 && ySet <= 190 ? ySet : 0
        })`;
      };
    };

    // 관찰 대상의 교차 상태(Boolean) 가 true이면 scrollMatrix실행
    if (entry.isIntersecting) {
      scrollMatrix();
    }
  }, []);

  useEffect(() => {
    let observer;
    // dom을 관찰 대상으로 설정
    const { current } = dom;
    // 관찰 대상의 전체가 보여지면({ threshold: 1 }) handleScroll 함수 호출
    if (current) {
      observer = new IntersectionObserver(handleScroll, { threshold: 1 });
      // observe() 함수 실행시 관찰 대상을 인자로 넣는다.
      observer.observe(current);

      // Q 왜 화살표 함수로?
      // A return 함수는 원래 화살표 함수로. 원래 여기서는 disconnet()를 해준다.
      return () => observer;
    }
  }, [handleScroll]);

  return {
    ref: dom,
    style: {
      opacity: 1,
    },
  };
};
```