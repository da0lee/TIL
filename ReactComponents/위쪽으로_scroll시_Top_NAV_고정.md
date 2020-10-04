> 소스폴더: 이솝

> Pages > Main > Components > CitrusFeed > CitrusFeed.js

> Components > Nav > Nav.js


<br/>


# window에 위쪽 방향으로 scroll시 top NAV고정

### CitrusFeed.js
```js
constructor() {
    super();
    // 세로스크롤 위치, 네브 고정여부 state 설정 
    this.state = {
      currentScrollY: 0,
      fixedNav: false,
    };
  }

  componentWillMount() {
    window.addEventListener("scroll", this.handleScroll);
  }

// Q unmount 시 removeEventListener 아닌가?
  componentWillUnmount() {
    window.addEventListener("scroll", this.handleScroll);
  }

// scroll 값이 달라질 때만 함수 실행
  componentDidUpdate(prevState) {
    const { currentScrollY } = this.state;
    if (prevState.currentScrollY !== currentScrollY) {
      if (currentScrollY === 0) {
        this.setState({ fixedNav: false });
      } else {
        if (prevState.currentScrollY < currentScrollY) {
          this.setState({ fixedNav: false });
        // 이전 scrollY값이 현재 scrollY값보다 크면 fixedNav: true
        } else {
          this.setState({ fixedNav: true });
        }
      }
    }
  }

  handleScroll = () => {
    const currentScrollY = window.scrollY;
    this.setState({ currentScrollY });
  };
```

<br/>

### Nav.js 

Nav에 state 전달
```js
 <Nav fixedNav={this.state.fixedNav} />
```