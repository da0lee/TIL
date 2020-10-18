> 소스코드 : prgrms-rct-5-class-3

> data > posts > reducers.js

<br/>

# Post 관련 reducer

```js
import { combineReducers } from 'redux';
import * as ActionTypes from '@/data/rootActionTypes';

const INITIAL_ENTITIES_STATE = {
  [0]: {
    seq: 0,
    writer: { name: 'Jason', profileImageUrl: 'https://www.gravatar.com/avatar/205e460b479e2e5b48aec07710c08d50' },
    contents: 'Hello guys! Have a good weekend. Learning React is really fun!',
    createAt: Date.now(),
    likes: 1,
    comments: 0,
    likesOfMe: true,
  },
};

// posts에 해당하는 entities와 posts의 id를 모아놓은 ids

function entities(state = INITIAL_ENTITIES_STATE, action = {}) {
  switch (action.type) {
    case ActionTypes.ADD_POST:
      return {
        // Q 어떻게 ...state 먼저 하고 새글을 추가했는데 기존 글 위에 새글이 쌓이지!
        ...state,

        // key의 갯수가 각 post의 id가 된다.
        [Object.keys(state).length]: {
          seq: Object.keys(state).length,

          // action에서 넘겨받은 payload user와 contents
          writer: action.user,
          contents: action.contents,
          createAt: Date.now(),
          likes: 0,
          comments: 0,
          likesOfMe: false,
        },
      };
    case ActionTypes.LIKE_POST: {
      const newLikedPost = { ...state[action.postId] };
      if (newLikedPost.likesOfMe === false) newLikedPost.likes += 1;
      newLikedPost.likesOfMe = true;
      return {
        ...state,
        [action.postId]: newLikedPost,
      };
    }
    default:
      return state;
  }
}

const INITIAL_IDS_STATE = [0];

function ids(state = INITIAL_IDS_STATE, action = {}) {
  switch (action.type) {
    case ActionTypes.GET_POSTS:
      return [...state];
    case ActionTypes.ADD_POST:
      return [state.length, ...state];
    default:
      return state;
  }
}

export default combineReducers({
  entities,
  ids,
});
```