> 소스코드 : prgrms-rct-5-class-3

<br/>

# 회원가입 입력단계 나누기

> pages > SignUp > helpers.js

<br/>

### helpers

```js
const STEPS = {
  EMAIL_PASSWORD: 0,
  PROFILE: 1,
};

export { STEPS };
```

<br/>

> pages > SignUp > index.js

<br/>

###  SignUp > index.js

```js
const renderForm = (step, setStep) => {
  switch (step) {
    case STEPS.EMAIL_PASSWORD:
      return <EmailPasswordForm setStep={setStep} />;
    case STEPS.PROFILE:
      return <ProfileForm setStep={setStep} />;
  }

  function SignUp() {
    // step state
    const [step, setStep] = useState(STEPS.EMAIL_PASSWORD);

    return (
      <div className="signup container">
        <h1 className="text-center">계정 만들기</h1>
        {renderForm(step, setStep)}
      </div>
    );
  }
};
```

<br/>

> pages > SignUp > EmailPasswordForm > index.js

<br/>

### EmailPasswordForm

```js
const EmailPasswordForm = ({ setStep }) => {
  const handleSubmit = (e) => {
    e.preventDefault();
    // 이메일, 비번 작성하고 '다음' 버튼 클릭, props로 받은 setStep로 step state변경
    setStep(STEPS.PROFILE);
  };
  return (
    <form onSubmit={handleSubmit}>
      <input type="email" className="form-control" placeholder="이메일" required />
      <input type="password" className="form-control" placeholder="비밀번호" minLength="5" required />
      <input type="password" className="form-control" placeholder="비밀번호 확인" required />
      <button className="btn btn-lg btn-primary btn-block" type="submit">
        다음
      </button>
    </form>
  );
};
```