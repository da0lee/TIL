# mySQL

![](https://www.practicalecommerce.com/wp-content/uploads/images/0001/6513/3-redo.jpg)   
출처: https://www.practicalecommerce.com/Databases-What-Online-Merchants-Need-to-Know

<br/>

- 가장 널리 사용되고 있는 관계형 데이터베이스 관리 시스템(RDBMS: Relational DBMS)이다.
- 표준 SQL 형식을 사용하므로, 데이터베이스에 대한 작업 명령은 SQL 구문을 이용하여 처리된다. 
- 오픈 소스이며, 다중 사용자, 다중 스레드를 지원한다.
- 다양한 운영체제 (Window, OS, Renux)에서 사용할 수 있으며, 여러 프로그래밍 언어를 위한 다양한 API를 제공하고 있다.
- 크기가 큰 데이터 집합도 아주 빠르고 효과적으로 처리할 수 있다.


  > 데이터베이스 : 대량의 정보를 컴퓨터가 효율적으로 접근할 수 있게 가공하고 저장해 놓은 것.    
  > SQL(Structured Query Language) : 데이터베이스에서 자료를 처리할 때 사용하는 구조화된 질의어.   
  > Table : 세로줄과 가로줄의 모델을 이용하여 정렬된 데이터 집합(값)의 모임.
  > 스키마(schema) : 테이블에 적재될 데이터의 구조와 형식을 정의 하는 것

  <br/>

## 타입(data type)
MySQL에서 테이블을 정의할 때는 필드별로 저장할 수 있는 타입까지 명시해야 한다.

### MySQL에서 제공하는 기본 타입

1. 숫자 타입
2. 문자열 타입
3. 날짜와 시간 타입

<br/>

## Node.js 서버와 연결

'mysql.createConnection()'을 이용해 DB와 서버를 연결하는 객체를 만들 수 있다.
이를 통해 각종 쿼리(Query)를 실행시킨다. 

<br/>

`참고`
- http://www.tcpschool.com/mysql/mysql_intro_intro
- https://ko.wikipedia.org/wiki/%ED%85%8C%EC%9D%B4%EB%B8%94_(%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4)