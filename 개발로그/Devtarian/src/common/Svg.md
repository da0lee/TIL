# 💻 SVG component

<br/>

> src > components > common > Svg.js

<br/>

- Q ) SVG를 어떻게 관리할까
- A ) 
  - 공통 component로 만들어 path에 내려주는 d 속성만 변수 처리하면 하나의 component로 여러 형태의 svg를 관리할 수 있다.

  - 이번 프로젝트에서는 운좋게 svg가 다 하나의 path로 이루어져 사용이 가능했지만, smile emoji처럼 여러 path로 이루어진 svg의 경우 이 component로 관리할 수 없다. 다음 프로젝트에서는 라이브러리를 쓰던가, data: 형태로 이루어진 svg를 찾아서 사용할 것 같다. 


<br/>

```js
import React from 'react';
import styled from 'styled-components';

// path의 d 속성 object로 관리
const svgObj = {
  ...

  arrow: 'M12 16l6-6H6z',
  cafe:
    'M20 3H4v10c0 2.21 1.79 4 4 4h6c2.21 0 4-1.79 4-4v-3h2c1.11 0 2-.9 2-2V5c0-1.11-.89-2-2-2zm0 5h-2V5h2v3zM4 19h16v2H4z',

  ...
};

// 부모 component에서 원하는 모양을 'type' props로 내려주고, svgObj에서 해당 'type'을 찾아 d 속성에 내려준다. (svgObj[type])
const Svg = React.forwardRef(({ className, type, color, ...rest }, ref) => {
  
  // 스펠링을 틀린다던가, svgObj에 정의되지 않은 type을 내려줬을 경우 오류가 날 수 있기 때문에 미리 return 시킨다.
  if (!svgObj[type]) return;

  return (
    <Wrapper
      className={className}
      ref={ref}
      type={type}
      {...rest}
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 24 24">
      <path fill={color || 'black'} d={svgObj[type]} />
    </Wrapper>
  );
});

export default Svg;

const Wrapper = styled.svg`
  width: ${(props) => (props.w ? props.w : '16px')};
  height: ${(props) => (props.h ? props.h : '16px')};
  margin: ${(props) => (props.m ? props.m : '0')};
  padding: ${(props) => (props.p ? props.p : '0')};
  border-radius: ${(props) => (props.radius ? props.radius : '0')};
  background: ${(props) => (props.bg ? props.bg : 'none')};
  color: ${(props) => (props.color ? props.color : 'black')};
  z-index: ${(props) => (props.zIndex ? props.zIndex : 0)};
  vertical-align: sub;
`;

```