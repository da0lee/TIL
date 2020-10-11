> 소스코드: 1week-prgrms-rct-5-class-1_reviewer 

<br/>

> components > Navigation > Index.js

```js
<ul className="nav">
  // props show에 user정보를 전달해서 해당 naviItem을 보여줄지 말지를 판단한다. (Hoc에서 관리)
  <NaviItem to="/login" text="로그인" show={!user} />
  <NaviItem to="/signup" text="회원가입" show={!user} />
  <Profile show={user} user={user} />
  <NaviItem to="/signout" action={onLogout} text="로그아웃" show={user} />
</ul>
```
<br/>

> components > Navigation > Index.js

```js
const NaviItem = ({ to, text, action }) => {
  const onClickAnchor = (e) => {
    // 각 <NaviItem/> 중 로그아웃 아이템에만 action={onLogout} 가 전달되었기 때문에 if(action)으로 분기 처리를 해준다.
    if (action) {
      e.preventDefault();
      e.stopPropagation();
      // 현재 초기 설정이 user에 harry라는 사용자 정보가 있는 상태이기 때문에 navItem을 클릭하면 user의 정보가 undefined로 설정되는 logOut함수가 실행된다.
      action();
    }
  };

  return (
    <li className="nav-item">
      <a href={to} onClick={onClickAnchor} className="nav-link">
        {text}
      </a>
    </li>
  );
};

// Hoc로 NaviItem 감싼다.
export default toggle(NaviItem);
```

<br/>

> hocs > toggle.js

```js
// 함수에 react component 전달
function toggle(WrappedComponent) {

  // <Navigation/>에서 <NaviItem/>로 전달했던 props 전달
  return function ToggleWrapped(props) {

    // show props가 true면 props를 그대로 전달하여 보여주고, 아니면 보여주지 않는다.
    // <NaviItem/>와 <Propfile/>을 Hoc으로 감쌌으므로 여기서 <WrappedComponent/>는 각각 <NaviItem/>와 <Propfile/> 나타낸다.
    return props.show ? <WrappedComponent {...props} /> : false;
  };
}
```