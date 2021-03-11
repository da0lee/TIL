# GraphQL

![](https://blog.cloud-elements.com/hs-fs/hubfs/calls.jpg?width=1044&height=597&name=calls.jpg)       
출처 : https://blog.cloud-elements.com/graphql-benefits-in-a-rest-api-but-how

<br/>

- 데이터에 접근하기 위한 질의 언어 중 하나이다. 사용자가 어떤 데이터가 필요한 지 명시할 수 있다는 특징을 갖고있다. 클라이언트가 필요한 데이터의 구조를 지정할 수 있고, 서버는 클라이언트가 지정한 것과 동일한 구조로 데이터를 반환한다. 

- REST API 같은 다른 웹서비스 아키텍쳐를 대체할 수 있다.

<br/>

## GraphQL을 사용하는 이유

### over-fetching의 해결

예를 들어 사용자가 로그인 시 '000님 안녕하세요 :)' 라는 문구를 헤더에 보여줄 경우, restAPI를 사용하면 이름, ID, email, 마지막 접속 일 등이 모두 담겨 있는 user 정보를 받아와서 그 중 id를 걸러내야 하지만, GraphQL을 사용하면 내가 원하는 user의 ID정보만 요청하고 받아올 수 있다.

반대로 상세 페이지 처럼 받아야하는 정보들이 많고, 딱 정해져 있는 경우에는 GraphQL에서 필요한 것을 하나하나 적어 요청하는 것보다 Rest API의 URL 한 줄로 적어 보내는 것이 유리하다.

<br/>

### under-fetching의 해결

방금 인스타그램에 로그인 했다고 가정해보자. 헤더에 내 아이디와 프로필이 뜨고, 알림이 오며, 메인 화면에는 내가 팔로잉 하는 사람들의 피드가 뜬다. 이 데이터들을 보여주기 위해서는 user, notifications, feeds 총 세 가지 정보가 필요하다. 이것을 Rest API로 요청한다면 서버와 3번의 통신이 필요하다. 즉 3번의 통신이 이루어져야 비로소 앱을 실행할 수 있다는 의미이다. GraphQL을 이용하면 내가 원하는 정보들을 한 query에 담아 단 한 번의 요청만으로 원하는 모든 정보들을 받아올 수 있다.

<br/>

> GraphQL 에서의 query : GraphQL(Graph Query Language)로 내가 원하는 정보를 database에 알려주고 요청할 수 있다.

<br/>

Rest API
```
/user/1/
/notifications/
/feeds/
```

<br/>

GraphQL
```js
// 요청 (GraphQL : Graph Query Language)

query {
  feed {
    comments
    likes
  }
  notifications {
    isRead
  }
  user {
    name
    profile
  }
}

// 응답 (JavaScript)

{
  feed : [
    {
      comments: 1
      likes: 10
    }
  ],
  notifications : [
    {
    isRead: true
    }
    {
    isRead: false
    }
  ],
  user : {
    name: 'dayoung'
    profile: 'http://'
  }
  
}
```

<br/>

> over-fetching : 내가 요청한 영역보다 많은 정보를 서버로 부터 받는 것. 리소스의 낭비가 발생한다.

> under-fetching : 하나의 endpoint로의 요청으로는 필요한 데이터를 완성하지 못해 서버에 여러 번 정보를 요청해야 하는 것. 추가적인 리소스 요청이 발생한다.

<br/>

## 조작 방식
- query : 데이터 조회
- mutation : 데이터 수정
- subscription : 실시간 어플리케이션 구현 시 사용

<br/>

## GraphQL vs  Rest API

### GraphQL
- 요청은 복잡하지만, 받는 데이터는 효율적이다.
- 모든 리소스가 그래프처럼 서로 연결되어있기 때문에 URL을 분리할 필요가 없다.  Query Language 입력을 받기 위한 단 하나의 Endpoint만이 존재한다.
- url이 아닌 Query를 통해 Resource를 표현하기 때문에, 서버는 Resource를 가져오는 Query, 어떤 Resource를 변경하기 위한 Mutation만 제공하면 된다.

<br/>

### Rest API
- 요청은 단순하지만, 받는 데이터가 복잡하다. 
- URL과 Resource를 매칭시키는 개념적 모델을 사용하기 때문에 수많은 Endpoint를 사용한다.


  > schema : 데이터베이스에서 자료의 구조, 표현 방법, 자료 간의 관계를 형식 언어로 정의한 구조이다.

<br/>

 `참고`    
 - https://ko.wikipedia.org/wiki/%EA%B7%B8%EB%9E%98%ED%94%84QL
 - https://tech.kakao.com/2019/08/01/graphql-basic/
 - youtube.com/watch?v=dGB0m7agxKE
 - https://www.youtube.com/watch?v=xiE9-S7s9rs
 - https://fourwingsy.medium.com/graphql%EC%9D%84-%EC%98%A4%ED%95%B4%ED%95%98%EB%8B%A4-3216f404134