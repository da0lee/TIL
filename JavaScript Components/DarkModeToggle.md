> 소스코드 : prgrms-devjs3-practice

> darkModeToggle.js

<br/>

# DarkMode Toggle 

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

<br/>
<hr/>
<br/>

### DarkMode Toggle 나의 풀이 1-1

```js
class DarkLightBtn {
  $darkLightBtn = null;
  osDarkMode = null;
  getColorMode = null;

  constructor({ $target }) {
    const $darkLightLable = document.createElement('label');
    const $darkLightBtn = document.createElement('input');
    const $darkLightSlider = document.createElement('span');
    this.$darkLightLable = $darkLightLable;
    this.$darkLightBtn = $darkLightBtn;
    this.$darkLightSpan = $darkLightSlider;

    $darkLightBtn.type = 'checkbox';
    $darkLightBtn.className = 'darkLightBtn';
    $darkLightSlider.className = 'darkLightSlider';

    $target.appendChild($darkLightLable);
    $darkLightLable.appendChild($darkLightBtn);
    $darkLightLable.appendChild($darkLightSlider);

    // localStorage에서 가져온 color-mode / light, dark
    this.getColorMode = localStorage.getItem('color-mode');

    // 지금 내가 짠 로직은 os의 darkmode가 사용자의 toggle 설정여부 보다 우위로 적용되고 있다.
    // os의 Darkmode 값을 여부로 localStorage에 color-mode 값을 저장할 것이 아니라 사용자의 toggle 클릭 여부를 기점으로 저장해야 한다. 
    // 최초 진입시 color-mode를 설정하기 위한 로직
    if (this.osDarkMode) {
    // os의 다크모드 설정여부. 값이 boolean으로 반환된다.
    this.osDarkMode = window.matchMedia && window.matchMedia('(prefers-color-scheme: Dark)').matches;

      document.documentElement.setAttribute('color-mode', 'dark');
      localStorage.setItem('color-mode', 'dark');
    } else {
      document.documentElement.setAttribute('color-mode', 'light');
      localStorage.setItem('color-mode', 'light');
    }

    $darkLightBtn.addEventListener('change', (e) => {
      this.getColorMode = this.getColorMode === 'light' ? 'dark' : 'light';
      document.documentElement.setAttribute('color-mode', this.getColorMode);
      localStorage.setItem('color-mode', this.getColorMode);
    });
  }
}
```

<br/>
<hr/>
<br/>

### DarkMode Toggle 나의 풀이 1-2

```js
// DarkLightBtn => DarkLightToggle
// 정확히는 button태그가 아닌 checkbox type의 input이다. 기능을 좀 더 직관적으로 드러내기 위해 toggle로 명칭 변경 
class DarkLightToggle {
  $darkLightLable = null;
  $darkLightBtn = null;
  $darkLightSlider = null;
  osDarkMode = null;
  getColorMode = null;

  constructor({ $target }) {
    const $darkLightLable = document.createElement('label');
    const $darkLightBtn = document.createElement('input');
    const $darkLightSlider = document.createElement('span');
    this.$darkLightLable = $darkLightLable;
    this.$darkLightBtn = $darkLightBtn;
    this.$darkLightSpan = $darkLightSlider;

    $darkLightBtn.type = 'checkbox';
    $darkLightBtn.className = 'darkLightBtn';
    $darkLightSlider.className = 'darkLightSlider';

    $target.appendChild($darkLightLable);
    $darkLightLable.appendChild($darkLightBtn);
    $darkLightLable.appendChild($darkLightSlider);

    this.getColorMode = localStorage.getItem('color-mode');

    this.initColorMode();

    $darkLightBtn.addEventListener('click', () => {
      this.setColorMode();
    });
  }

  initColorMode() {
    // boolean으로 반환된 것을 'dark' : 'light';로 변형해 getColorMode와 맞춰주었다.
    this.osDarkMode = window.matchMedia && window.matchMedia('(prefers-color-scheme: Dark)').matches ? 'dark' : 'light';
    console.log(this.osDarkMode);

    if (this.getColorMode) {
      document.documentElement.setAttribute('color-mode', this.getColorMode);
    } else {
      // 위에서 osDarkMode와 getColorMode의 type을 맞춰주었으므로 분기처리가 줄어들었다.
      document.documentElement.setAttribute('color-mode', this.osDarkMode);
    }
  }

  setColorMode() {
    this.getColorMode = this.getColorMode === 'light' ? 'dark' : 'light';
    document.documentElement.setAttribute('color-mode', this.getColorMode);
    localStorage.setItem('color-mode', this.getColorMode);
  }
}
```