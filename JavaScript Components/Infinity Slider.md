# Infinity Slider


## HTML
```html
<div class="slider_wrap">
  <ul class="slider">
    <li><img src="http://placehold.it/800x300.png?text=A" alt=""/></li>
    <li><img src="http://placehold.it/800x300.png?text=B" alt=""/></li>
    <li><img src="http://placehold.it/800x300.png?text=C" alt=""/></li>
  </ul>
  <div class="slider_arrow">
    <a href="" class="arrow prev">&lt;</a>
    <a href="" class="arrow next">&gt;</a>
  </div>
</div>
```

<br/>

## CSS
ul.slider를 position으로 띄워 보여줄 화면을 left로 조정
```css
/* reset */
* {
  margin:0; 
  padding:0;
  box-sizing: border-box;
  }
li {list-style: none;}
img {display:block}
a {text-decoration: none}

/* slider */
.slider_wrap {
  position:relative;
  max-width: 800px;
  height:300px;
  margin:0 auto;  
  overflow:hidden;
  border:2px solid black; 
  }
.slider_wrap .slider {
  position:absolute;
  left:0;
}
.slider_wrap .slider > li {float:left;}
.arrow {
  z-index: 1;
  position: absolute; 
  top:40%;
  font-size: 25px
}
.slider_wrap .slider_arrow > .prev {left:20px;}
.slider_wrap .slider_arrow > .next {right:20px;}
```

<br/>

## Java Script

<br/>

### window.onload = fucntion() {}

<br/>

https://webdir.tistory.com/515

문서의 모든 콘텐츠(images, script, css, etc)가 로드된 후 발생하는 event

- 문서에 포함된 모든 콘텐츠가 로드된 후에 실행되기에 불필요한 로딩시간이 추가될 수 있다.
- 동일한 문서에 오직 onload는 하나만 존재해야 하며, 중복될 경우 마지막 선언이 실행된다.
- 외부 라이브러리에서 이미 선언된 경우 이를 찾아 하나로 합치는 과정이 필요하다.

<br/>

### [[Environment]]

<br/>

https://ko.javascript.info/closure     
https://velog.io/@surim014/JavaScript-Closure%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80

모든 함수는 함수가 생성된 곳의 렉시컬 환경을 기억한다. 함수는 [[Environment]]라 불리는 숨김 프로퍼티를 갖는데, 여기에 함수가 만들어진 곳의 렉시컬 환경에 대한 참조가 저장된다.

호출 장소와 상관없이 함수가 자신이 태어난 곳을 기억할 수 있는 건 바로 [[Environment]] 프로퍼티 덕분이다. [[Environment]]는 함수가 생성될 때 딱 한 번 그 값이 세팅되고, 이 값은 영원히 변하지 않는다.

아래 moveSlider()를 호출하면 각 호출마다 새로운 렉시컬 환경이 만들어진다. 그리고 이 렉시컬 환경은 moveSlider.[[Environment]]에 저장된 렉시컬 환경을 외부 렉시컬 환경으로서 참조하게 된다.

변숫값 갱신은 변수가 저장된 렉시컬 환경에서 이뤄진다. 따라서 moveSlider()를 여러 번 호출하면 외부의 변수가 2, 3으로 계속 증가하게 된다.

```js
// window.onload
// window.onload를 하지 않으면, clientWidth를 찍어봐도 css에 값을 먹이기 전 default인 0이 들어온다. 이 작업을 해줘야 원하는 element의 clientWidth를 얻을 수 있다.
 window.onload = function() {
    const slider = document.querySelector('ul.slider')
    const sliderLis = slider.querySelectorAll('.slider li')
    const liWidth = sliderLis[0].clientWidth
    const sliderWidth = liWidth * sliderLis.length

    slider.style.width = `${sliderWidth}px`

    const sliderArrows = document.querySelector('.slider_arrow')
    sliderArrows.addEventListener('click', moveSlider)

    // Call Stack
    // 0. GC에 window.onload = function() {}
    // 1. window.onload라는 scope 안에 querySelector로 찾은 DOM들, sliderArrows에 addEventListener, 2번의 moveSlider scope에서 이용하는 변수 moveDist, currentIndex 선언
    // 2. 1번의 callback 함수인 moveSlider()

    // moveSlider()는 자신이 선언됐을 때의 환경 Scope를 기억하고 접근할 수 있다. (본인이 기억하고 있는 주변 상황에 대한 정보를 지속적으로 감지.)
    // 그렇기에 moveSlider() 외부에 moveDist, currentIndex를 선언 한 후 moveSlider() 함수 내부에서 변수 값을 변경하는 로직을 짜면, click을 할 때마다 moveSlider()가 실행되며 moveDist, currentIndex의 값이 바뀌게 된다. (Closer 이용)
    // moveSlider() 안쪽에 변수를 선언하게 되면, 마찬가지로 자신이 선언됐을 때의 환경 Scope를 기억하기 때문에 한 번 0으로 참조한 값이 변하지 않는다.
  
    const INIT_INDEX = 0
    const INIT_DIST = 0
    let currentIndex = INIT_INDEX
    let moveDist = INIT_DIST

    setSliderLeft() {
      slider.style.left = `${moveDist}px`;
    }

    function moveSlider(e) {
      e.preventDefault()
      if (e.target.classList.contains('prev')) {
        // prev arrow를 눌렀는데 맨 앞 페이지 일 때 
        if (currentIndex === INIT_INDEX) {
          currentIndex = sliderLis.length -1
          moveDist = -(liWidth * currentIndex)
          setSliderLeft()
        } else {
          currentIndex -= 1
          moveDist += liWidth
          setSliderLeft()
        }       
      } else {
        // next arrow를 눌렀는데 맨 마지막 페이지 일 때
        if (currentIndex === sliderLis.length -1) {
          currentIndex = INIT_INDEX
          moveDist = INIT_DIST
          setSliderLeft()
        } else {
          currentIndex += 1
          moveDist -= liWidth
          setSliderLeft()
        }
      }
    }
  }
```