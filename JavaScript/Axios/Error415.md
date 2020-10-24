> 소스코드 : prgrms-rct-5-class-4-reviewer-clone

<br/>

# join - 415 error

https://lkhlkh23.tistory.com/88

https://qastack.kr/programming/45578844/how-to-set-header-and-options-in-axios

https://sangcho.tistory.com/entry/axios

## ContentType (String, default : application/x-www-form-urlencoded)

- ContentType은 클라이언트가 전송하는 데이터의 형식이다. ConetentType을 지정하지 않으면 default는 application/x-www-form-urlencoded

- 타입으로 서버에 요청을 보내고, 서버는 JSON 형식으로 데이터를 읽으려고 하다보니 415 오류가 발생한다.

<br/>

> services > apis > client.js

join 요청이 가고,

error: {message: "Content type 'application/json;charset=UTF-8' not supported", status: 415} 에러떠서 아래 코드 추가했지만 여전히 에러

### 추가 코드1

```js
const socialApiClient = axios.create({
  baseURL: SOCIAL_SERVER_URL,
  headers: { 'Content-Type': 'application/json;charset=UTF-8' },
});
```

<br/>

### 추가 코드2

```js
axios.defaults.headers.post['Content-Type'] = 'application/json;charset=UTF-8';
```

<br/>

> services > apis > users > index.js

```js
  async register({ email, password, profileImage, name }) {
    try {
      const res = await socialApiClient.post('/api/user/join', { email, password, profileImage, name });
      return res.data.response;
    } catch (e) {
      throw Error(e.message);
    }
  },
```
