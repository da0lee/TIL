
# matchProps	

- match/ location/ history 와 같이 브라우저 라우팅에 관련된 데이터, 함수를 가지는 객체이다.	
- ...matcProps => 예전엔 이렇게 해야했지만 지금은 useHistory hook로 쓸 수 있다.


### Login 페이지일 떄 PublicLayout이 받는 props	

App.js에서 props 전달하고,	

```js	
    <Router>	
        <Switch>	
          <PublicLayout path="/login" component={Login} className="login" />	
          <PublicLayout path="/signup" component={SignUp} className="signup" />	
          <DefaultLayout path="/" component={Home} className="posts" />	
        </Switch>	
```	

<br/>	

PublicLayout.js 에서 받는다.	

```js	
const PublicLayout = ({ component: Component, className, ...rest }) => {	
  console.log({ Component, className, rest });	
  return (	
    <Route	
      {...rest}	
      render={	
        (matchProps) => console.log(matchProps)	
        // <>	
        //   <div className={className ? 'container ' + className : 'container'}>	
        //     <Component {...matchProps} />	
        //   </div>	
        // </>	
      }	
    />	
  );	
};	
```	

<br/>	

- console.log	

```js	
{className: "login", rest: {…}, Component: ƒ}	
//  Component	
Component: ƒ Login()	
arguments: (...)	
caller: (...)	
length: 0	
name: "Login"	
prototype: {constructor: ƒ}	
__proto__: ƒ ()	
[[FunctionLocation]]: Login.js:4	
[[Scopes]]: Scopes[2]	
//  className	
className: "login"	
// rest	
rest:	
computedMatch: {path: "/login", url: "/login", isExact: true, params: {…}}	
location: {pathname: "/login", search: "", hash: "", state: undefined, key: "w2czh4"}	
path: "/login"	
__proto__: Object	
__proto__: Object	
```	
<br/>	
```js	
// matchProps	
{history: {…}, location: {…}, match: {…}, staticContext: undefined}	
history: {length: 6, action: "POP", location: {…}, createHref: ƒ, push: ƒ, …}	
location: {pathname: "/login", search: "", hash: "", state: undefined, key: "w2czh4"}	
match: {path: "/login", url: "/login", isExact: true, params: {…}}	
staticContext: undefined	
__proto__: Object	
```