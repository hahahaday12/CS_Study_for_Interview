# Network
![image](https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/125563995/c42edea8-c7ec-45ed-bae0-f9964b552a45)

## Request Headers

- 요청헤더

  - HTTP 요청 헤더는 서버로 요청할 데이터의 정보가 담겨있는 헤더
  - HTTP 요청에서 사용되지만 메시지의 컨텐츠와는 관련이 없음
  - Fetch될 리소스나 클라이언트 자체에 대한 정보를 포함

---

- 대표적으로 사용되는 Http request headers
  - Host
    - 서버의 도메인 네임과 서버가 현재 Listening 중인 TCP 포트를 지정
    - 만약 포트가 지정되지 않는다면 요청된 서버의 기본 포트를 의미
    - Host 헤더는 반드시 하나가 존재해야 하며 만약 한개가 아니거나 여러개라면 400 error 발생
  - User-Agent
    - 현재 사용자가 어떤 클라이언트(운영체제와 브라우저를 포함한)를 이용해 요청을 보냈는지 확인
  - Accept
    - Accept는 요청을 보낼 때 서버에게 어떤 터입으로 응답을 보내줬으면 좋겠다고 명시
    - `Accept: text/html` 을 요청 헤더로 보내면 HTML 형식인 응답을 처리
    - 다음과 같은것들을 포함해서 보낼수 있음
      - Accept-Charset : 원하는 Character Set
      - Accept-Language : 원하는 Lang
      - Accept-Encoding : 원하는 Encoding 방식
  - Authorization
    - 사용자가 서버에 인가된 사용자임을 증명할 때 사용
    - JWT나 Bearer 토큰을 서버로 보낼 때 사용하며 자격이 증명되지 않을 경우 401 Unauthorized 상태를 알려줌
    ```
    Authorization: <type> <credentials>
    Authorization: Basic YWxhZGRpbjpvcGVuc2VzYW1l
    ```
    - type : 인증 타입으로 보통 Basic과 Bearer을 사용한다
    - credentials : 사용자명과 비밀번호, 다른 페이로드가 합처져 복호화된 값
  - Origin
    - POST와 같은 요청을 보낼 때, 요청이 어느 주소에서 시작되었는지를 나타냄
    - 여기서 요청을 보낸 주소와 받는 주소가 다르면 CORS 문제가 발생함
