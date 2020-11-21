# 1. window.onload = fucntion() {}

<br/>

https://webdir.tistory.com/515
https://webclub.tistory.com/630 

문서의 모든 콘텐츠(images, script, css, etc)가 로드된 후 발생하는 event

- 문서에 포함된 모든 콘텐츠가 로드된 후에 실행되기에 불필요한 로딩시간이 추가될 수 있다.
- 동일한 문서에 오직 onload는 하나만 존재해야 하며, 중복될 경우 마지막 선언이 실행된다.
- 외부 라이브러리에서 이미 선언된 경우 이를 찾아 하나로 합치는 과정이 필요하다.

+) 이렇게 head hag 안에 script를 위치시키고 script 에 defer나 async를 적용시켜도 html을 모두 load한 후 script 파일을 읽어오므로 같은 효과를 볼 수 있다.


# 2. defer 
HTML 구문 분석이 완전히 완료되면 스크립트 파일을 실행하도록 브라우저에 지시.

# 3. async 
HTML 구문 분석과 병행하여 비동기적으로 script를 가져온 후 script가 준비 될 때마다 즉시 실행이 가능하다.

실행의 순서가 다운로드 완료 시점의 결정되므로 실행 순서가 중요한 script를에 async 를 사용할 때는 유의해야 한다.

<br/>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" type="text/css" href="./Slider.css" />
    <!-- defer, async-->
    <script type="text/javascript" src="./Slider.js" defer></script>
    <script type="text/javascript" src="./Slider.js" async></script>
    <title>Slider</title>
  </head>
</html>
