> 소스폴더: 이솝

> Pages > Main > Components > Carousel > Carousel.js


<br/>

# 수동 Carousel

```js
class Carousel extends React.Component {
  constructor() {
    super();
    this.state = {
      items: [],
      currentItemIdx: 0,
      shownItems: [],
      // 이전버튼 false
      shownPrev: false,
      // 다음버튼 true
      shownNext: true,
    };
  }

  componentDidMount() {
    this.handleInitData();
  }

  componentDidUpdate(prevProps, prevState) {
    const { currentItemIdx } = this.state;

    if (prevState.currentItemIdx !== currentItemIdx) {
      // currentItemIdx가 0이면 이전 버튼 숨기기
      if (currentItemIdx === 0) this.setState({ shownPrev: false });
      // currentItemIdx가 4이면 다음 버튼 숨기기
      else if (currentItemIdx === 4) this.setState({ shownNext: false });
      else this.setState({ shownPrev: true, shownNext: true });
    }
  }

  handleInitData = () => {
    fetch("http://localhost:3000/data/maindata.json")
      .then((res) => res.json())
      .then((res) => {
        if (res.result === "SUCCESS") {
          this.setState({ items: res.data });
        }
      });
  };

  prevSlide = () => {
    const { items, currentItemIdx } = this.state;
    const resetToVeryBack = currentItemIdx === 0;
    // 맨 뒤까지 도달했으면 이전 버튼을 눌렀을 때 (전체 아이템 수-1)이 currentItemIdx고, 아직 도달하기 전 이면 (현재 index에서 -1)이 currentItemIdx이다.
    // Q 1-1) 그런데 왜 resetToVeryBack이  currentItemIdx === items.length - 1이 아니라 currentItemIdx === 0 인지는 모르겠다.
    const index = resetToVeryBack ? items.length - 1 : currentItemIdx - 1;
    this.setState({ currentItemIdx: index });
  };

  nextSlide = () => {
    const { items, currentItemIdx } = this.state;
        // Q 1-2) 마찬가지
    const resetIndex = currentItemIdx === items.length - 1;
    const index2 = resetIndex ? 0 : currentItemIdx + 1;
    this.setState({ currentItemIdx: index2 });
  };

  itemsToDisplay = () => {
    const { items, currentItemIdx } = this.state;
    const createSources = items.slice(currentItemIdx, currentItemIdx + 3);
    return createSources;
  };

 // 캐러셀 박스 안에 cursor가 위치할 때만 이전 / 다음 버튼 보여주기
 // 화살표를 숨길 땐 cursor를 올렸을 때 아무 반응도 없어야하는데 여전히 커서 기능이 유효하다. 이부분은 좀 성기게 짠 것 같다.
  cursorInArrows = () => {
    const { currentItemIdx } = this.state;
    if (currentItemIdx === 0) {
      this.setState({
        shownPrev: false,
        shownNext: true,
      });
    } else if (currentItemIdx === 4) {
      this.setState({
        shownPrev: true,
        shownNext: false,
      });
    } else {
      this.setState({ shownPrev: true, shownNext: true });
    }
  };

  cursorOutArrows = () => {
    this.setState({
      shownPrev: false,
      shownNext: false,
    });
  };

  render() {
    const itemList = this.itemsToDisplay();

    return (
      <>
        <div className={this.props.firstFeed ? "Carousel" : "HiddenCarousel"}>
          <div
            className="itemCarousel"
            onMouseEnter={this.cursorInArrows}
            onMouseLeave={this.cursorOutArrows}
          >
            <div className="btnWrapper">
              <button
                className={
                  this.state.shownPrev ? "prevBtn " : "prevBtnIsHidden"
                }
                onClick={this.prevSlide}
                disabled={this.state.shownPrev ? "" : "disabled"}
              >
                <svg role="img" viewBox="0 0 50 50">
                  <g>
                    <polygon points={aesopLogoPath.slideArrow}></polygon>
                  </g>
                </svg>
              </button>
            </div>
            <div className="listedItem">
 
              {itemList.map((el) => (
                <div className="eachItem">
                  <img alt="" src={el.image_url} />
                  <p>{el.product__name}</p>
                  <p className="briefDesc">{el.product__description}</p>
                </div>
              ))}
            </div>
            <div className="btnWrapper">
              <button
                className={
                  this.state.shownNext ? "nextBtn " : "nextBtnIsHidden"
                }
                onClick={this.nextSlide}
                disabled={this.state.shownNext ? "" : "disabled"}
              >
                <svg role="img" viewBox="0 0 50 50">
                  <g>
                    <polygon points={aesopLogoPath.slideArrow}></polygon>
                  </g>
                </svg>
              </button>
            </div>
          </div>
        </div>
      </>
    );
  }
}
export default Carousel;
```