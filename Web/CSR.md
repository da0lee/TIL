# CSR (Client Side Rendering) / SSL (Server Side Rendering)

> TTV (Time to View) : 사용자가 웹사이트를 볼 수 있는 시점
> TTI (Time to Interactive): 사용자가 웹사이트와 상호작용할 수 있는 시점

<br/>

## CSR (Client Side Rendering)

<br/>

## Rendering 과정

![](https://www.infidigit.com/wp-content/webp-express/webp-images/doc-root/wp-content/uploads/2020/08/Picture2.jpg.webp)

출처: https://www.infidigit.com/blog/server-side-rendering-vs-client-side-rendering/

<br/>

1. 사용자가 사이트에 접속
2. Server로 부터 텅빈 index 파일을 받아온다. (사용자가 아직 아무것도 볼 수 없다.)
3. 2번의 HTML에 link되어져 있는 이 웹사이트에서 필요한 모든 js 로직들 다운로드한다.
4. 동적으로 HTML을 생성할 수 있는 웹어플리케이션 로직이 담긴 js파일을 받아온다 (ex. react) 사용자가 웹사이트를 볼 수 있고, 상호작용할 수 있다. (TTV, TTI)

<br/>

### 특징
1. Server는 빈 HTML만 보내주고, Client 측에서 렌더링을 한다.
2. 검색 엔진 봇이 텅빈 HTML을 읽기 때문에 SEO가 어렵다. -> 각 url 마다 필요한 js파일을 쪼개는 code spliting으로 해결 가능
3. TTV, TTI가 일치하므로, 사용자가 첫 화면을 보기까지 시간이 오래걸린다.
4. url이 변경돼도 HTML을 새로 내려주지 않기 떄문에 인터렉션이 빠르고, 페이지 깜빡거림이 없다.

<br/>

## SSL (Server Side Rendering)

<br/>

## Rendering 과정

![](https://www.infidigit.com/wp-content/webp-express/webp-images/doc-root/wp-content/uploads/2020/08/Picture1.jpg.webp)

출처: https://www.infidigit.com/blog/server-side-rendering-vs-client-side-rendering/

<br/>

1. 사용자가 사이트에 접속
2. server에서 이미 잘 만들어진 index 파일을 받아온다. (TTV, 사용자가 웹사이트를 볼 수 있지만, 아직 동적으로 제어할 수 있는 js파일을 받아오지 않았으므로 인터렉션이 불가능하다.)
3. 2번의 HTML에 link되어져 있는 이 웹사이트에서 필요한 모든 js 로직들 다운로드한다.
4. 동적으로 HTML을 생성할 수 있는 웹어플리케이션 로직이 담긴 js파일을 받아온다 (ex. react) 
사용자가 웹사이트와 상호작용할 수 있다. (TTI)

<br/>

## 특징

1. Server에서 이미 잘 만들어진 index 파일을 받아와 Client 측에서는 그려주기만 한다.
2. 모든 콘텐츠가 HTML에 담겨져 있기 때문에 SEO가 효율적이다.
3.  TTV와 TTI 사이에 시차가 존재하므로, 페이지는 보이지만 사용자가 그것을 이용할 수는 없는 공백 시간이 생긴다.
4. 깜빡거림 이슈가 있다.
5. 요청과 응답이 많이 일어나는 사이트의 경우, server에 과부하가 걸리기 쉽다.

<br/>

## SSG (Static Site Generation)

Next.js를 이용하면, 첫 페이지는 SSR을 이용하고, 그 이후의 인터렉션에 대해서는 Link, Rout 등을 통해 CSR로 처리할 수 있다. 