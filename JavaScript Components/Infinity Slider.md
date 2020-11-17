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
// 개발자 도구의 network에서 살펴보면, html는 읽혔지만 (script가 포함된)아직 image가 읽혀지기 전이기 때문에 width가 0이 찍혔다. 이 때 image를 await하거나 window.onload를 해주면 image의 clientWidth를 얻을 수 있다.
 window.onload = function() {
    const slider = document.querySelector('ul.slider')
    const sliderLis = slider.querySelectorAll('.slider li')
    const liWidth = sliderLis[0].clientWidth
    const sliderWidth = liWidth * sliderLis.length

    slider.style.width = `${sliderWidth}px`

    const sliderArrows = document.querySelector('.slider_arrow')
    sliderArrows.addEventListener('click', moveSlider)

    // Call Stack
    // 0. Global Execution context에 window.onload = function() {}, addeventListener. addeventListener은 1번이 아닌 0번에 존재한다. sliderArrows가 DOM이기 때문에. 마찬가지로 click event에 대한 call back함수인 moveslider도 0번에 적재되어있다.
    // 1. window.onload라는 scope 안에 querySelector로 찾은 DOM들, 2번의 moveSlider scope에서 이용하는 변수 moveDist, currentIndex 선언
    // 2. 1번의 callback 함수인 moveSlider(). moveslide()는 0번 stack window의 addeventListener를 통해 탑재된 callback함수이므로 0번 stack에 적재되어있으나, 실행하면 2번 stack이 쌓이게 된다.

    // moveSlider()는 자신이 선언됐을 때의 환경 Scope를 기억하고 접근할 수 있다. (본인이 기억하고 있는 주변 상황에 대한 정보를 지속적으로 감지.)
    // 그렇기에 moveSlider() 외부에 moveDist, currentIndex를 선언 한 후 moveSlider() 함수 내부에서 변수 값을 변경하는 로직을 짜면, click을 할 때마다 moveSlider()가 실행되며 moveDist, currentIndex의 값이 바뀌게 된다. moveslide()에서 사용해야하기 때문에 currentIndex,moveDist는 없어지지 않고 살아있기 때문이다. (Closer 이용)
    // 함수가 실행되어 일을 처리하고, 종료되면 그 안에서 참조하던 값들도 사라지기 때문에 moveSlider() 안쪽에 변수를 선언하게 되면, 함수 종료 후 moveDist, currentIndex를 찾을 수 없다. 따라서 변경도 불가하다.
  
    const INIT_INDEX = 0
    const INIT_DIST = 0
    let currentIndex = INIT_INDEX
    let moveDist = INIT_DIST

    moveSliderLeft() {
      slider.style.left = `${moveDist}px`;
    }

    function moveSlider(e) {
      e.preventDefault()
      if (e.target.classList.contains('prev')) {
        // prev arrow를 눌렀는데 맨 앞 페이지 일 때 
        if (currentIndex === INIT_INDEX) {
          currentIndex = sliderLis.length -1
          moveDist = -(liWidth * currentIndex)
          moveSliderLeft()
        } else {
          currentIndex -= 1
          moveDist += liWidth
          moveSliderLeft()
        }       
      } else {
        // next arrow를 눌렀는데 맨 마지막 페이지 일 때
        if (currentIndex === sliderLis.length -1) {
          currentIndex = INIT_INDEX
          moveDist = INIT_DIST
          moveSliderLeft()
        } else {
          currentIndex += 1
          moveDist -= liWidth
          moveSliderLeft()
        }
      }
    }
  }
```