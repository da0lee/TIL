# Uncaught ReferenceError: regeneratorRuntime is not defined

https://programmingsummaries.tistory.com/401

Babel은 ES2015+ 문법을 ES5 지원 Browser에서 해석할 수 있도록 변환해주는 트랜스파일러다. 하지만 새롭게 추가된 전역객체들 (지금 여기서는 Axios)는 트랜스파일링 만으로는 해결하기 어렵기 때문에 core-s나 regenerator-rnuntime과 같은 별도의 polyfill이 필요하다.

<br/>

### yarn add -D yarn babel-plugin-transform-runtime

<br/>

설치 후 babelrc 수정

> .babelrc

```js
{
  "presets": ["@babel/preset-react", "@babel/preset-env"],
  "plugins": [
    ["styled-jsx/babel", { "optimizeForSpeed": true, "vendorPrefixes": true, "sourceMaps": false }],
    "@babel/plugin-transform-runtime",
    [
      "module-resolver",
      {
        "root": ["./src"]
      }
    ]
  ]
}
```