> 소스코드 : 3week_prgrms-rct-5-class-3

<br/>

# 특정 User의 게시글만 filter한 페이지

> pages > User > index.js

```js
const User = () => {
  const dispatch = useDispatch();
  const postsState = useSelector(selectors.posts.getPosts);
  const location = useSelector(getLocation);

  // const userName = props.computedMatch?.params?.name; 로도 구할 수 있다.
  // location.pathname 이 있다면 (/u/Jason), /u/를 제외한 글자만 추출하고, 추추한 단어 앞에 아무 것도 붙히지 않는다. ('')
  const userName = location?.pathname?.replace(/\/u\//, '');

  // nomarization : postsState 안에 post 정보의 모음에 해당하는 entities와 post 정보들의 id들만 모아놓은 ids가 따로 있다
  // ids에 map을 돌린다.
  // postsState의 데이터 모음인 entities에서 일치하는 id를 찾아 filter한 것이 posts.
  const posts = useMemo(
    () => postsState.ids.map((id) => postsState.entities[id]).filter((each) => each?.writer?.name === userName),
    [postsState.entities, postsState.ids]
  );

  // posts state에 map을 돌려 각 Post item들을 생성
  // useName에 따라 filter 내용이 달라지므로 두번째 인자에 userName이 필요하다.
  const postList = useMemo(() => posts.map((post) => <Post key={post.seq} post={post} />), [posts, userName]);

  // <User/> mount 되기 전 posts 정보 불러와 업데이트
  useEffect(() => {
    dispatch(actions.posts.getPosts());
  }, []);

  return (
    <div className="container">
      {postList}
      <style jsx>{`
        .container {
          max-width: 600px;
        }
      `}</style>
    </div>
  );
};
```