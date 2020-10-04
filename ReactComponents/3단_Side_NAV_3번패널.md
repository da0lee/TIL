> 소스폴더: 이솝

> Components > Nav > SkinSideBar.js

> Components > Nav > SkinDetail.js


<br/>

# 3단 Side Nav - 3번 패널

### SkinSideBar.js

Sidebar 2번 패널에 마우스 onMouseEnter event 일어날 시 해당 카테고리의 3번 패널 보여주기
```js
  openThird = (e) => {
    this.setState({ shownThird: true, categoryKey: e.target.id });
  };
```
<br/>

SkinDetail (Sidebar 3번 component)에 skinCategory, categoryKey 전달
```js
{shownThird && (
          <SkinDetail skinCategory={skinCategory} categoryKey={categoryKey} />
        )}
```
<br/>

### SkinDetail.js

```js
class SkinDetail extends React.Component {
  render() {
    // data 정보
    const { skinCategory, categoryKey } = this.props;

    // categoryKey가 1부터 시작하므로 -1
    const matchingIdx = Number(categoryKey) - 1;

    return (
      <div className="SkinDetail">
        <div className="panelList showAll">
          <Link className="panelLink" to="/">
            {skinCategory[matchingIdx].name} 모두 보기
          </Link>

          // matchingIdx와 일치하는 스킨카테고리 보여주기

          {skinCategory[matchingIdx].product.map((el) => (
            <ul className="productInfo" id={el.id}>
              <Link className="productLink" to="/">
                <li>
                  <div className="infoDesc">
                    <span className="panelLink infoName">{el.name}</span>
                    {el.size.length > 1 ? (
                      <span>2 사이즈 / {el.size[0].price} 부터 </span>
                    ) : (
                      <span>
                        {el.size[0].size} / {el.size[0].price}
                      </span>
                    )}
                  </div>
                  <div className="infoImgContainer">
                    <img className="infoImg" alt="product" src={el.image_url} />
                  </div>
                </li>
              </Link>
            </ul>
          ))}
        </div>
      </div>
    );
  }
}
```