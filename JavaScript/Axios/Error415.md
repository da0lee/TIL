> 소스코드 : prgrms-rct-5-class-4-reviewer-clone

<br/>

# join - 415 error

```
{message: "Content type 'application/json;charset=UTF-8' not supported", status: 415}
```

<br/>

내가 주는 data와 server가 받을 수 있는 data 형식이 다를 때 발생한다.

<br/>

## 해결1 : header에 Content type 정의

<br/>

https://lkhlkh23.tistory.com/88

https://qastack.kr/programming/45578844/how-to-set-header-and-options-in-axios

<br/>

## ContentType (String, default : application/x-www-form-urlencoded)

- ContentType은 클라이언트가 전송하는 데이터의 형식이다. ConetentType을 지정하지 않으면 default는 application/x-www-form-urlencoded다.

- 타입으로 서버에 요청을 보내고, 서버는 다른 형식(ex. JSON 형식)으로 데이터를 읽으려고 하면 415 오류가 발생한다.

<br/>

> services > apis > client.js

join 요청이 가고,

error: {message: "Content type 'application/json;charset=UTF-8' not supported", status: 415} 에러떠서 아래 코드 추가

### 방법1

```js
const socialApiClient = axios.create({
  baseURL: SOCIAL_SERVER_URL,
  headers: { 'Content-Type': 'application/json;charset=UTF-8' },
});
```

<br/>

### 방법2

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

<br/>

보통은 위 방법으로 해결이 가능한데, 나의 경우 server가 읽을 수 있는 데이터 형식이 json이 아니었으므로 해결되지 않았다.

<br/>
<hr>
<br/>

## 해결 2 :  new FormData

<br/>

server가 읽을 수 있는 형식으로 데이터 변환

<br/>

> services > apis > users > index.js

```js
async register({ principal, credentials, name, profileImage }) {
  const formdata = new FormData();
  formdata.append('credentials', credentials);
  formdata.append('principal', principal);
  formdata.append('file', profileImage);
  formdata.append('name', name);

  try {
    const res = await socialApiClient.post('/api/user/join', formdata);
    return res.data.response;
  } catch (e) {
    throw Error(e.message);
  }
},
```

<br/>

> data > users > actions.js 

이 server는 email을 principal로, password을 credentials로 주어야 읽을 수 있다.

```js
export const register = ({ email, password, profileImage, name }) => async (dispatch) => {
  console.log(email, password, profileImage, name);
  try {
    await apis.usersApi.register({
      principal: email,
      credentials: password,
      name,
      profileImage,
    });
    // TODO: After finishing the mission of week 4, we should save user in Redux after register
    dispatch(actions.router.push('/'));
  } catch (error) {
    alert(error.message);
  }
};
```

<br/>

회원가입 요청 성공!