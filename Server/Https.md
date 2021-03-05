# Https
 Hypertext Transfer Protocol Over Secure Socket Layer의 약자. HTML을 전송하기 위한 통신규약(Http) 중 보안(s)이 강화된 것이다. 
 
 ## 장점
 1. 내가 사이트에 보내는 정보들을 제 3자가 보지 못하게 한다.
 2. 접속한 사이트가 믿을 만한 곳인지 알려준다.

## SSL 통신과정

![](https://i.imgur.com/YIfy1wK.png)

출처: https://wayhome25.github.io/cs/2018/03/11/ssl-https/

<br/>

### 1. HandShake

1-1. `Client`    
- Client Hello
- client가 server에 접속한다.
- server에게 전달하는 정보 :
  1) client가 생성한 랜덤 데이터
  2) client가 지원하는 암호화 방식들 : browser, version마다 지원하는 암호화 방식이 다르기 때문에 client는 server에게 자신이 지원하는 암호화 방식 후보를 전달 해 상호 간에 어떤 암호화 방식을 사용할 것인지 협상 한다.
  3) 세션 아이디 : 이미 SSL 핸드쉐이킹을 했다면 비용과 시간을 절약하기 위해서 기존의 세션을 재활용한다. 이 때 사용할 '연결에 대한 식별자'를 server로 전송한다.

1-2. `Server`   
- Server Hello
- server에게 전달하는 정보 :
  1) server가 생성한 랜덤 데이터
  2) server가 선택한 암호화 방식 : client가 전달한 암호화 방식 중 server에서도 사용할 수 있는 암호화 방식을 선택해 client에게 전달한다. server와 client는 이 암호화 방식을 이용해서 정보를 교환하게 된다.
  3) 해당 server의 인증서

1-3. `Client`    
- server가 보내온 인증서가 진짜인지 확인하기 위해 browser에 내장된 CA 리스트를 확인한다.
  - CA의 인증을 받은 인증서들은 해당 CA의 개인키로 암호화 되어있기 때문에, 인증서가 진짜라면 해당 browser에 내장 되어있는 CA의 공개키로 복호화가 가능하다. 성공적으로 복호화된 인증서에는 해당 server의 공개키가 포함되어 있다.
  - 복호화에 성공하면 인증서를 전송한 server는 믿을만한 server이다. 인증서가 CA 리스트에  없다면 사용자에게 경고 메시지를 보낸다.
- 위 1,2번에서 client와 server가 생성한 랜덤 데이터를 조합해서 pre master secret Key (대칭키)를 생성한다.
  - 이 임시키를 server로 부터 받은 인증서에 담겨있던 공개키로 암호화해서 server에 전송한다.
  (데이터는 대칭키를 사용해 암호화 하고, 그 암호화 된 데이터를 공유할 때 공개키를 사용한다.)
  - 이 key는 나중에 세션 단계에서 주고받는 데이터를 암호화하기 위해서 사용된다.
  
> * 공개키를 인증 방식은 대칭키에 비해 컴퓨터에 많은 부담을 주기 때문에, 전부 공개키 인증 방식을 사용하지 않고 두 방식을 섞어서 통신한다.

1-4. `Server`
- 자신의 비공개키로 client가 전송한 pre master secret 값을 복호화한다.
  - server, client 모두 pre master secret 값을 공유하게 되었다.
- 대칭키 (session key)를 생성한다.
  - server, client는 모두 일련의 과정을 거쳐 pre master secret 값을 master secret 값으로 만든다. master secret은 대칭키(session key)를 생성하는데, server와 client는 이 대칭키를 이용해서 정보를 암호화 한 후에 주고 받는다.

1-5. `Client` / `Server`
- 핸드쉐이크 단계의 종료를 서로에게 알린다.
 
<br/>

### 2. Session

실제로 server와 client가 데이터를 주고 받는 단계.    
 대칭키(session key)를 이용해서 암호화한 정보를 상대방에게 전송한다.

 <br/>

### 3. Session 종료
데이터 전송이 완료되면 SSL 통신이 끝났음을 서로에게 알리고, 통신에서 사용한 대칭키를 폐기한다.

<br/>

 `참고`
 - https://opentutorials.org/course/228/4894
 - https://www.youtube.com/watch?v=H6lpFRpyl14
 - https://wayhome25.github.io/cs/2018/03/11/ssl-https/