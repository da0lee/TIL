> 소스코드 : prgrms-devjs3-practice

> darkModeToggle.js

<br/>

### DarkMode Toggle 

```js
class DarkModeToggle {
  // state

  isDarkMode = null;

  // element 생성, event 등록,

  constructor({ $target }) {
    const $DarkModeToggle = document.createElement('input');
    this.$DarkModeToggle = $DarkModeToggle;
    this.$DarkModeToggle.type = 'checkbox';

    $DarkModeToggle.className = 'DarkModeToggle';
    $target.appendChild($DarkModeToggle);

    $DarkModeToggle.addEventListener('change', (e) => {
      this.setColorMode(e.target.checked);
    });
    this.initColorMode();
  }

  // 활용할 함수들 정의
  // constructor 안에 있어도 동작하지만, 더 깔끔하게 코드륵 작성하기 위해 바깥 쪽에 함수로 분리
  // this.isDarkMode의 경우 지금처럼 직접 할당하는 것보다 setState() 를 사용하는 것이 좋다.

  initColorMode() {
    // 초기화
    // isDarkMode state, checked 상태, html attribute
    this.isDarkMode = window.matchMedia('(prefers-color-scheme:dark)').matchs;
    // os의 darkmode 여부에 따라 우리가 만든 toggle btn의 클릭상태 결정
    this.$DarkModeToggle.checked = this.isDarkMode;
    this.setColorMode(this.isDarkMode);
  }

  // os의 darkmode 여부에 따라 body의 color-mode 설정
  setColorMode(isDarkMode) {
    document.documentElement.setAttribute('color-mode', isDarkMode ? 'dark' : 'light');
  }

  render() {}
}
```