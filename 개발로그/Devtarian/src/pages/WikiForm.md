# 💻 WikiForm

## 📂1-1 UploadImg Component의 reRendering 방지 

<br/>

> src > pages > wikiForm > WikiForm.js

<br/>

- Q ) 부모 Component의 다른 state 변경 시 하위 Component의 rerendering 방지
- A ) 
  1. UploadImg를 React.memo()로 감싼다.
  2. UploadImg에 넘겨주는 값을 useMemo()로 감싼다.
  - https://leehwarang.github.io/2020/05/02/useMemo&useCallback.html
  - `<WikiForm/>`에서 titile, contents 등의 input 값이 바뀌면 Component의 state 값이 변경되는 것이므로 Component가 rerendering된다. 이 때 `<WikiForm/>`의 하위 component인 `<UploadImg/>` 또한 마찬가지 인데,  1, 2번을 거치면 넘겨주는 props가 변경되지 않을 경우 부모 Component인 `<WikiForm/>`가 rerendering 되더라도, `<UploadImg/>`는 rerendering 되지 않는다. 

<br/>

> src > components > form > UploadImg.js
```js
const UploadImg = ({ name, imgUrls, onImageUpload }) => {

  ...

};

export default React.memo(UploadImg);
```

<br/>

> src > pages > wikiForm > WikiForm.js
```js
  const imgUrls = useMemo(() => changeFileToImgUrl(inputs.files, inputs.imgUrls), [inputs.files, inputs.imgUrls]);
```

<br/>

## 📂1-2  changeFileToImgUrl() 에 전달 parameter가 두 개인 이유

- Q ) changeFileToImgUrl() 에 전달 parameter가 두 개인 이유
- A ) 

<br/>

```js
const INIT_WIKIPOST = {
  category: 'processed',
  product: '',
  ingredient: '',
  info: EditorState.createEmpty(),
  files: [],
};

const WikiForm = ({ match }) => {

  const { inputs, setInputs, errors, onInputChange, onImageUpload, requiredValidate } = useInput(INIT_WIKIPOST);

// form의 이미지 등록 초깃값이 최초 등록일 때는 files이고, 편집일 때는 data가 server에서 넘어오므로 imgUrls로 넘어온다. 그래서 changeFileToImgUrl() 함수에 값을 두 개 넘겨주어 선택적으로 사용하게 한다. 
  const imgUrls = useMemo(() => changeFileToImgUrl(inputs.files, inputs.imgUrls), [inputs.files, inputs.imgUrls]);

  useEffect(() => {
    // 위키편집이 아닐 경우 아직 wikiId가 없을 것이므로 return한다.
    if (!wikiId) return;
    apis.wikiApi.getWikiDetail(wikiId).then((res) => {
      setInputs({
        category: res.category,
        product: res.product,
        ingredient: res.ingredient,
        imgUrls: res.imgUrls,
        info: EditorState.createWithContent(ContentState.createFromBlockArray(convertFromHTML(res.info))),
        files: [],
      });
    });
  }, [setInputs, wikiId]);

  };

  ...

};

export default WikiForm;


```
