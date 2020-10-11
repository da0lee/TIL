> 소스코드 : 1주차 페이스북_ji

> services > PostService.js

<br/>

# 새 comment의 seq값 부여하기

기존 seq 값보다 1 큰 seq 값으로 새로운 comment 입력

seq1을 삭제하여 seq 2,3,4 만 존재하는 상태에서는 전체 length인 3+ 1을 하여 새 seq가 4가 되므로 allCommentList.length + 1로는 정확하지 않다.

```js
allCommentList.reduce((seq, comment) => Math.max(seq, comment.seq), 0) + 1;
```