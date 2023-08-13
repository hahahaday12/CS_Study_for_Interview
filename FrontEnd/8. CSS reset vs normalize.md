## Problem
브라우저들마다 HTML의 기본 스타일링이 조금씩 다르다. 
같은 `<h1>` 태그라도 브라우저마다 크기나 마진이 다를 수 있다. 

CSS `reset`과 `nomalize`는 **cross browsing**을 위한 방법 중 HTML의 스타일을 동일하게 적용되기 위한 방법이다.

`reset`은 매우 잘 알려저 있으며 Eric Meyer의 Reset.css를 복붙하여 사용하거나, CDN을 사용하는 방법 등이 있다. 
그러나 상대적으로 `normalize`는 생소하다.

브라우저별 스타일 일관성을 위한 두 방법에 대해 알아보고 두 방법의 차이점과 장단점에 대해 알아보자.

## resetting vs normalizing

### Reset
- 모든 브라우저 스타일을 `초기화` 한다.
- `h1`과 `span`의 차이가 없다.
- 장점
  - 익숙한 방법. 
- 단점
  - 표준화된 방법이 없다.
  - 스타일이 의미를 지니는 경우 초기화된 스타일로 인해 구분이 되지 않음.
    
    ![](https://velog.velcdn.com/images/junsgk/post/896794f9-8bc6-4981-bdc4-99eff5d13790/image.png)

### Normalize
- 브라우저 스타일을 초기화 시키는 것이 아니라 모든 브라우저에서 똑같이 보이도록 한다. 
- `h1`은 `h1`처럼 보임
- 장점
  - 일관된 스타일을 보여줘야하는 크로스브라우징의 목적에 부합함
  - 태그 본연의 스타일이 내포하는 의미를 전달 할 수 있음. `<h1>은 글자가 크고 굵어! 중요한 내용이야!`
  ![](https://velog.velcdn.com/images/junsgk/post/5cda6f3a-c159-432d-b8a2-8d6ac659d8aa/image.png)
  - 지속적으로 업뎃 중인 공동 프로젝트.
  https://github.com/necolas/normalize.css
  - 필요한 부분만 선별적으로 normalize 할 수 있으며 설명이 잘 되어있음.
- 단점
  - 익숙하지 않음
  
## 결론 및 고찰
- 스타일링 통일화를 위한 방법이 reset만 있는 것이 아니다.
- 장단점을 알고 상황에 맞게 사용
- MUI(material UI)의 경우 다음과 같이 스타일을 reset한다.
```js
import * as React from 'react';
import CssBaseline from '@mui/material/CssBaseline';

export default function MyApp() {
  return (
    <React.Fragment>
      <CssBaseline />
      {/* The rest of your application */}
    </React.Fragment>
  );
}
```
- Tailwind css의 경우 설치시 자동으로 css를 reset한다.
