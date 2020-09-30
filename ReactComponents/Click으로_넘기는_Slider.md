> 소스폴더: kinfork

> Pages > Main > Main.js

> Pages > Main > MainComponents > SlideCotents.js


<br/>

# Click으로 넘기는 Slider

 BookPhotoBox에 ref 지정하고 translateX() 로 가로 방향으로 이동하는데,
 이동값은 - (전체 슬라이드 수에서 현재 ref의 width값을 나눈값) * (현재 슬라이더)의 px     

* (-) 를 하면 오른쪽으로 이동 

 -${
        (slideRef.current.clientWidth / TOTAL_SLIDES) * currentSlider
      }px

<br/>

### [SlideCotents.js] Slider 이동 width 설정

```js
export default function SlideCotents({
  BookPhoto,
  currentSlider,
  setCurrentSlider,
  nextSlide,
  PrevSlide,
  slideRef,
  TOTAL_SLIDES,
}) {

  // props 안에 들어있는 value 값이 바뀔 때에만 특정 작업을 수행
  // Q TOTAL_SLIDES, slideRef는 변하는 값이 아니니까 [] 안에 안 넣어줘도 되지 않나?


  useEffect(() => {
    if (slideRef) {
      slideRef.current.style.transition = "all 0.5s ease-in-out";
      slideRef.current.style.transform = `translateX(-${
        (slideRef.current.clientWidth / TOTAL_SLIDES) * currentSlider
      }px)`;
    }
  }, [TOTAL_SLIDES, currentSlider, slideRef]);

  return (

    <div>
      <SlideCotentsContainer>
        <PrevSlideButton onClick={PrevSlide} />
        <BookPhotoWrapper>
          <BookPhotoBox ref={slideRef}>
            {BookPhoto &&
              BookPhoto.map((el, index) => (
                <BookPhotoSize key={index}>
                  <img alt="slidePhoto" src={el.src} />
                </BookPhotoSize>
              ))}
          </BookPhotoBox>
        </BookPhotoWrapper>
        <NextSlideButton onClick={nextSlide} />
      </SlideCotentsContainer>
      <NotionPart>
        <span>
          From wilderness to windowsill: Plant roots in the world around you.
        </span>
        <KinfolkButton>Buy Now</KinfolkButton>
      </NotionPart>
    </div>
  );
}
```
<br/>

### [ Main.js ] nextSlide / PrevSlide       

```js
  const nextSlide = () => {
    if (currentSlider >= TOTAL_SLIDES) {
      setCurrentSlider(0);
    } else {
      setCurrentSlider(currentSlider + 1);
    }
  };

  const PrevSlide = () => {
    if (currentSlider === 0) {
      setCurrentSlider(TOTAL_SLIDES);
    } else {
      setCurrentSlider(currentSlider - 1);
    }
  };
```