# CSR (Client Side Rendering) / SSL (Server Side Rendering)

## CSR (Client Side Rendering)

### 단점
1. 사용자가 첫 화면을 보기까지 시간이 오래걸릴 수 있다.
2. SEO를 최적화 하지 못한다.

server에 접속 -> server에서 index 파일을 받아온다.

## SSL (Server Side Rendering)

1. 첫페이지 로딩이 빠르다
2. 모든 콘텐츠가 HTML에 담겨져 있기 때문에 SEO가 효율적이다.

1. 깜빡거림 이슈가 있다.
2. server에 과부하가 걸리기 쉽다.
3. 동적으로 인터렉션을 처리하는 JavaScript를 아직 받지 못해서 클릭해도 아무런 반응이 없다

server에 접속하면 이미 잘 만들어진 index 파일을 받아오게 된다.