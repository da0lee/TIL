> 소스코드 : 1week-prgrms-rct-5-class-1_reviewer

> pages > Home > PostForm.js

<br/>

# Disabled
  
- disabled 속성이 명시된 <input/> (input) 요소는 사용할 수 없으며, 사용자가 클릭할 수도 없다.
- 특정 조건이 충족될 때까지 사용자가 입력 필드를 클릭할 수 없도록 설정하고, 특정 조건이 충족되면 자바스크립트 등으로 disabled 속성값을 삭제하여 사용자가 입력 필드를 다시 사용할 수 있도록 조절할 수 있다.

```html
<!-- 양쪽 공백을 제외한 contents의 length가 존재하면 disabled 해제 -->
  <button type="submit" className="btn btn-primary" disabled={!contents.trim().length}>
```