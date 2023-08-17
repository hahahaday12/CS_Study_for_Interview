*배경지식이 필요한 부분이라서 SOP를 넣었습니다!*

# SOP(Same Origin Policy)
> 다른 출처(origin)의 리소스를 사용하는 것을 제한하는 보안 방식

### Origin이란?
  - URL의 protocol, host(domain), port를 통해 정함
  - `https://` `github.com` `:3000`/howooking
  - 이중 하나라도 다르면 다른 출처로 인식함
### why? 예시

  - 패캠 `https://fastcampus.com`은 로그인만 하여도 추가적인 인증절차없이 강의를 결제할 수 있다고 가정하자.
  - 패캠에 로그인을 하면 패캠에서는 인증토큰을 보내주고 브라우저에 저장된다.
  - 해커가 나에게 `http://hacker.com`로 접속을 유도한다.
  - 해커가 만든 사이트의 html, css, js가 내 브라우저에 받아진다.
  - 해커는 js에 나의 인증토큰을 담아 패캠에게 모든 강의를 결제하라는 코드를 심는다.
  - 이 때 패캠은 `http://hacker.com`로부터 결제 요청을 받게된다.
  - 브라우저는 요청의 origin을 확인하고 SOP에 따라 요청을 막는다.

### problem

  - 선량한 개발자인 나는 모든 인강 정보를 보여주는 사이트`https://lectures.com`를 만들고자 한다.
  - 패캠의 모든 강의목록을 불러오는 api(있다고 가정)를 통해 요청을 하게 되면 똑같은 문제가 발생
  - 다른 출처의 리소스가 필요하다면 어떻게 할까? 👉 CORS
 
# JSONP(JSON with padding)
- CORS가 나오기 전(2009년)에 사용했던 방법 SOP를 우회하는 방법
- HTML `<script>` 요소의 경우 외부 출처로부터 조회된 내용을 실행하는 것이 허용되는 특성(맹점)을 이용
- `GET` 요청만 가능
- CORS가 생긴 후에는 사용할 이유가 없음. 보안적인 이유로 거의 사용되지 않음
- 서버에서 허용해줘야 사용가능
- JSON 데이터를 클라이언트가 지정한 콜백 함수를 호출하는 유효한 Javascript 문법으로 감싸(with padding!) 클라이언트에게 전송하는 방법
- 뭔소린지 모르겠으니 코드를 보도록 하자.

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>JSONP 예시</title>
  </head>
  <body>
    <h1>서울 날씨</h1>
    <span>온도 : </span>
    <span id="temp"></span><br />
    <span>습도 : </span>
    <span id="humid"></span>
    <script>
      function handleWeatherData(data) {
        const temp = document.getElementById('temp');
        temp.innerText = data.main.temp;
        const humid = document.getElementById('humid');
        humid.innerText = data.main.humidity;
      }
    </script>
    <script src="https://api.openweathermap.org/data/2.5/weather?q=Seoul&appid=오픈웨더에서무료APIkey를받을수있어요!&units=metric&callback=handleWeatherData"></script>
  </body>
</html>

```
- api endpoint를 브라우저에 입력해보면 다음과 같이 나온다.

![](https://velog.velcdn.com/images/junsgk/post/26eac436-39ce-40ce-9106-b39cfe4c1d39/image.png)

- 지정한 `handleWeatherData` 함수 안에 json 값이 담겨져있다. 이 함수 실행문이 통째로 클라이언트에게 전달이 되고 클라이언트에서 선언한 `handleWeatherData` 함수가 실행된다.

![](https://velog.velcdn.com/images/junsgk/post/69159ed4-b185-4496-99b8-ae1725a51882/image.png)



# CORS
- 원래 다른 출처로부터 데이터를 주고 받는 것은 SOP에 의해 금지되어있으나 웹 생태계가 다양해지면서 여러 서비스들간의 데이터 교환이 필요해졌고 이를 위해 CORS가 등장.
- Cross Origin Resource Sharing, 다른 출처의 자원을 공유
- HTTP헤더를 사용하여 한 origin에서 다른 origin의 자원에 접근할 수 있는 권한을 부여하도록 `브라우저`에 알려주는 체제. postman에서는 되는데 브라우저에서는 에러가 나는 이유

