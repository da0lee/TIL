> 소스코드 : prgrms-rct-5, 2week_prgrms-rct-5-class-2_junil_working

<br/>

# input 입력시 자동으로 높이 늘어나는 Custom Hook

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