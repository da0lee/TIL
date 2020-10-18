> 소스코드 : prgrms-rct-5, 2week_prgrms-rct-5-class-2_junil_working

<br/>

# input 입력시 자동으로 높이 늘어나는 Custom Hook 1

> hooks > useAutoFormHeight.js

### Custom Hook
```js
import { useCallback, useEffect } from 'react';

export const useAutoFormHeight = (ref) => {
  useEffect(() => {
    const handleFormHeight = () => {
      const { scrollHeight, clientHeight, style } = ref.current;
      if (scrollHeight !== clientHeight) {
        style.height = `${scrollHeight}px`;
      }
    };
    ref.current?.addEventListener('input', handleFormHeight);
    return () => {
      ref?.current?.removeEventListener('input', handleFormHeight);
    };
  }, [ref]);

  const handleFormHeightSubmit = useCallback((e) => {
    const { name, style } = ref.current;

    e.preventDefault();
    name === 'post' ? (style.height = '100px') : (style.height = '50px');
  }, []);

  return { handleFormHeightSubmit };
};
```

<br/>

> components > comment > CommentForm.js

### CommentForm.js

```js
import { useAutoFormHeight } from '../../../hooks/useAutoFormHeight';

const RefCommentTextArea = useRef(null);
const { handleFormHeightSubmit } = useAutoFormHeight(RefCommentTextArea);

const handleCommentSubmit = useCallback(
  (e) => {
    e.preventDefault();
    onAddComment(seq, comment);

    // custom hook에 이벤트 전달
    handleFormHeightSubmit(e);
    setComment('');
  },
  [onAddComment, comment, handleFormHeightSubmit]
);

 <form className="comment-form" onSubmit={handleCommentSubmit}>
        <textarea
          // ref 설정
          ref={RefCommentTextArea}
          className="form-control input-lg"
          placeholder="댓글을 입력하세요..."
          spellCheck="false"
          value={comment}
          onChange={handleCommentsChange}
          // 각 post, comment일 때 높이를 다른 값으로 reset하기 위해 name 속성 추가 
          name="comment"
        />
        <button type="submit" className="btn btn-primary">
          댓글달기
        </button>
      </form>
```
<br/>
<hr/>
<br/>

> 소스코드 : prgrms-rct-5-class-3

<br/>

# input 입력시 자동으로 높이 늘어나는 Custom Hook 2

> hooks > useAutoHeight.js

```js
import { useRef, useLayoutEffect } from 'react';

export default function useAutoHeight(lineHeight, contents) {
  const ref = useRef(null);

  //height를 두번주면 reflow가 두번 일어나지만 이 정도는 괜찮지 않나 싶다
  useLayoutEffect(() => {
    const { style, scrollHeight } = ref.current;
    style.height = 'auto';
    style.height = `${scrollHeight}px`;
  }, [contents]);

  return [ref];
}
```

<br/>

> pages > Home > PostForm.js

```js
import useAutoHeight from '@/hooks/useAutoHeight';

const PostForm = (props) => {
  // 가변값 props로 구조 분해 할당하여 설정하여 다시 해당 함수에 props로 내려줌
  const { minHeight = 100, lineHeight = 20, placeholder = '무슨 생각을 하고 계신가요?' } = props;

  const [contents, setContents] = useState('');
  const dispatch = useDispatch();
  const userState = useSelector(selectors.users.getUser);

  // 참조 객체 자체를 생성하는 custom hook이므로 함수에 필요한 값 전달해서 textareaEl를 생성하여 ref에 할당해준다.
  const [textareaEl] = useAutoHeight(lineHeight, contents);

  const writePost = useCallback(
    (contents) => {
      dispatch(actions.posts.writePost(contents, userState));
    },
    [userState]
  );

  return (
    <form
      className="write-form"
      onSubmit={(e) => {
        e.preventDefault();
        writePost(contents);
        setContents('');
      }}>
      <textarea
        className="form-control input-lg"
        placeholder={placeholder}
        spellCheck="false"

        // ref 설정
        ref={textareaEl}
        value={contents}
        onChange={(e) => setContents(e.target.value)}
      />
      <button type="submit" className="btn btn-primary" disabled={!contents.trim().length}>
        공유하기
      </button>

      <style jsx global>{`
        .write-form > textarea.form-control {

          // style jsx에 props 내려준다.

          min-height: ${minHeight}px;
          line-height: ${lineHeight}px;
          padding: 20px;
          font-size: 18px;
          resize: none;
          border: none;
          border-radius: 0.5rem;
          transition: box-shadow ease-in-out 1s;
        }
        .write-form > textarea:focus {
          box-shadow: #999999 0 0 50px;
        }
        .write-form > button.btn {
          float: right;
          margin-bottom: 0;
          margin-top: 16px;
          background-color: #3b5999;
          color: #fffffe;
          border: none;
          font-weight: 800;
        }
        .write-form {
          margin-bottom: 100px;
        }
      `}</style>
    </form>
```