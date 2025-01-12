# SPA에서 SEO에 유리하도록 만들기 위한 방법에 대해 설명해주세요.

# SPA란?

## SPA(Single Page Application)<br/>
-> SPA는 서버로부터 새로운 페이지를 가져오는 것이 아닌,  하나의 페이지에서 내용을 동적으로 변경함으로써 사용자 웹앱<br/>

* 이전 사용했던 방식<br/>
## MPA(Multi Page Application)<br/>
->  다른 페이지로 넘어갈 때 URL도 바뀌고 서버로 들어가는 요청에 응답으로 html 파일을 건네서 완전히 새로운 페이지로 넘어감.<br/>
-> 웹사이트를 보면 레이아웃은 그대로이고 내용만 바뀜. 따라 그리지 않아도 되는 html까지 전달되어 트래픽 증가 되고 느려지는 단점.<br/>

---------

## SPA 장점<br/>
### 1.구조<br/>
-> SPA는 하나의 페이지로 구성된다. 초기에 필요한 모든 리소스를 로드하고, 이후에는 필요한 데이터만 비동기적으로 가져와 화면을 업데이트.<br/>
### 2.페이지 이동<br/>
-> SPA에서는 페이지 이동이 브라우저의 주소 표시줄을 변경하지 않고 JavaScript를 사용하여 화면을 업데이트. <br/>
이로 인해 전통적인 다중 페이지 애플리케이션과 비교하여 화면 깜박임이 줄어들고 빠른 사용자 경험을 제공할 수 있다.<br/>
### 3.서버 요청<br/>
-> SPA는 초기에 필요한 리소스를 로드한 후에는 서버에 요청하는 횟수가 줄어든다. 필요한 데이터만 비동기적으로 가져와 화면을 업데이트하므로 서버 요청이 최적화될 수 있음.<br/>
### 4.자바스크립트<br/>
-> SPA는 JavaScript를 중심으로 동작하며, 클라이언트 측에서 렌더링을 처리. 주로 JavaScript 프레임워크나 라이브러리 (예: React, Angular, Vue.js)를 사용하여 구현된다.<br/>

## SPA 단점<br/>
1. 처음 접속시에 사이트 구성과 관련된 모든 리소스를 한 번에 받기 때문에 초기 구동 속도가 느릴 수 있다.<br/>
2. 데이터를 별도로 요청하고 받아와서 화면을 구성하므로 설계 방식에 따라서는 화면이 변하는 모습이 사용자에게 노출될 수 있다. <br/>
3. SPA 구조 상 데이터 처리는 클라이언트에서 하는 경우가 많은데, 중요한 비즈니스 로직이 존재하는 중에 클라이언트가 정보를 볼수있다는점(개발자 도구)<br/>
4. 검색엔진 최적화(SEO)가 어렵다.<br/>

------

# SEO (Search Engine Optimization) 란?<br/>
->  웹사이트와 웹페이지를 검색엔진이 쉽게 발견하고, 읽고, 색인하고(인덱싱), <br/>
상위 노출(랭킹)시켜 자연 유입되는 트래픽의 양과 질을 높일 수 있도록 관련 검색 알고리즘의 특성을 고려해서 웹사이트의 구조나 콘텐츠를 개선하는 일련의 작업을 뜻함<br/>

## 1. 검색 엔진 인덱싱<br/>
-> 검색 엔진은 웹사이트의 컨텐츠를 인덱싱하여 검색 결과 페이지에 표시함. 전통적인 웹사이트는 HTML 페이지를 정적으로 렌더링하므로 검색 엔진이 컨텐츠를 쉽게 수집하고 인덱싱할 수 있다.<br/>
## 2. 동적 렌더링<br/>
-> SPA는 초기에는 비어있는 HTML을 로드하고, JavaScript를 사용하여 동적으로 컨텐츠를 렌더링. 검색 엔진 크롤러가 JavaScript를 실행할 수는 있지만, 모든 검색 엔진이 이를 완벽하게 지원x.<br/>
## 3. 메타 데이터<br/>
-> 검색 엔진은 메타 데이터를 사용하여 페이지의 제목, 설명, 이미지 등을 이해하고 검색 결과에 표시. SPA에서는 페이지 이동 시에도 메타 데이터를 동적으로 업데이트해야함.<br/>

#### => SEO 측면에서는 검색 엔진이 SPA의 동적인 특성을 이해하고 크롤링하는 것이 일반적인 정적 웹페이지보다 더 어려울 수 있다

## ✨ 어떻게 SPA에서 SEO에 유리하도록 할까? ✨

### 가장 흔한 방식<br/>
### 서버 사이드 렌더링(SSR): <br/>
서버 사이드 렌더링(SSR)을 사용. SSR은 서버에서 초기 페이지 로딩 시에 미리 렌더링하여 완성된 HTML을 브라우저로 전달하는 방식. <br/>
이를 통해 검색 엔진 크롤러는 완전한 컨텐츠를 읽을 수 있으며, 페이지의 검색 엔진 노출이 향상될 수 있다.<br/>

### 프리 렌더링(Pre-rendering): <br/>
-> 빌드 단계에서 각 페이지를 미리 렌더링하여 정적인 HTML 파일을 생성하는 방식. <br/>
이는 SPA의 동적인 특성을 유지하면서도 검색 엔진이 읽을 수 있는 HTML을 제공. Next.js와 Nuxt.js와 같은 프레임워크는 이러한 기능을 제공.<br/>

### 메타 데이터와 Open Graph 태그 활용: <br/>
-> SPA에서 페이지 이동 시에는 주로 JavaScript로 렌더링되기 때문에 초기 HTML에는 제한적인 정보만 포함될 수 있다. <br/>
검색 엔진에게 더 많은 정보를 제공하기 위해 메타 데이터와 Open Graph 태그를 사용하여 페이지 제목, 설명, 이미지 등을 설정할 수 있다.<br/>

------

### 🤔 프리 렌더링(Pre-rendering) 이란?

-> 리액트로 만든 페이지에 javascript 를 끄게 되면 빈페이지로 출력되는 경우 있음 <br/>
<img width="500" alt="image" src="https://github.com/hahahaday12/WinkBook/assets/101441685/933c3998-238e-4c71-98d4-c7c71f44f005"><br/>
<img width="500" alt="image" src="https://github.com/hahahaday12/WinkBook/assets/101441685/e536a50f-4f25-4ad9-8a1b-622fde168fa5"><br/>

-> 서버사이드 렌더링으로 데이터를 받아오는 상세 페이지는 자바스크립트를 꺼도 잘 보임<br/>
-> next.js에선 화면렌더링이 되면 초기에 만들어둔 html 파일이 렌더된다!이후에 js가 로드 되며 기능적인 컴포넌트들이 생겨난다!<br/>

### 🤔 메타 데이터란?
### 메타 태그: 
-> 웹 페이지의 <head> 섹션에 추가되는 메타 태그를 사용하여 페이지의 제목, 설명, 키워드 등을 정의할 수 있다. <br/>
이 정보는 검색 결과 페이지에 표시되며, 사용자에게 페이지의 내용을 간략하게 소개해줍니다.<br/>
-> 메타 데이터는 검색 엔진 크롤러가 페이지를 색인할 때 활용된다. <br/>
페이지의 내용을 파악하고, 어떤 키워드와 관련된 내용인지를 이해하는 데 도움을 줌.<br/>
-> Html <meta> 태그는 웹페이지에 나타나지 않고, 검색 엔진이나 웹크롤러를 통해 수집.<br/>
-> 구글 검색엔진은 웹 페이지에 대한 추가적인 정보를 얻기 위해 메타 데이터 사용.<br/>

### 🤔  Open Graph 태그 활용이란?
-> 인터넷 프로토콜의 한 종류로서 2010년에 페이스북이 발표.<br/>
오픈 그래프의 목적은 웹페이지에 대한 정보를 담고 있는 메타데이터의 사용방식을 표준화하여 링크 공유 시 해당 웹페이지에 대한 정보를 특정 형식의 미리보기 형태로 제공해주는 기능을 모든 웹페이지에서 가능하게끔 하는 것<br/>

<img width="500" alt="image" src="https://github.com/hahahaday12/WinkBook/assets/101441685/40e0e846-596f-4ce3-9604-ecba5ecd9115"><br/>

-> 직접적인 영향을 주지는 않지만, 오픈태그를 활용할때 사용자 유입, 전환률 영향을 준다. 












