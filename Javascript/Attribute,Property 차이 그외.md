# 속성와 요소의 차이 

## Attribute 란?
-> html 문서에서 elements 에 추가적인 정보를 넣을때 사용되는 요소. 

<img width="500" alt="image" src="https://github.com/hahahaday12/WinkBook/assets/101441685/2d6a2138-9661-4e87-89ca-e99ed97613df"> <br/>
-> 여기서 div 태그는 element(요소)이고, class는 attribute(속성) 이 되며, container 는 Value(값)이 된다. 

## Property 란?
-> 특성이란 뜻을 지닌 property는 html dom 안에서 attribute를 나타내는 표현. 

------
## ex) Attribute  예시

<img width="500" alt="image" src="https://github.com/hahahaday12/WinkBook/assets/101441685/207da8c0-66e9-4657-b8b7-5e768e008f33"> <br/>
-> JavaScript라는 것이 생겨난 것은 애초에 정적인 문서인 HTML을 동적으로 동작할 수 있게끔 하기 위한 것. 그러한 동적인 속성을 부여하는 것이 바로 property 이다.

<img width="500" alt="image" src="https://github.com/hahahaday12/WinkBook/assets/101441685/856882ff-1ec5-421d-aaab-190edc89bf57"><br/>
-> html dom 안에서는 Class가 attribute 를 의미.

<img width="500" alt="image" src="https://github.com/hahahaday12/WinkBook/assets/101441685/ab3a308c-f126-499b-b9a2-182a9e02f4ee">

------
## 차이점의 예시
```js
<div class="container">
  <input value="default">입력</input>
</div>
```
-> 위와 같이 코드를 작성하였을때, 

<img width="500" alt="image" src="https://github.com/hahahaday12/WinkBook/assets/101441685/4e79b5be-0fab-48c2-8b79-dfa65aa05273"><br/>
<img width="300" alt="image" src="https://github.com/hahahaday12/WinkBook/assets/101441685/7f27aa0a-37fc-4265-aeff-6993f4a54bd8"><br/>
->  input의 attribute 중 value 값은 'default'이고, DOM의 property  value 값 또한 'default'이다. 

## 🤔 input 필드 안의 내용을 변경시켜주어보면?<br/>
<img width="300" alt="image" src="https://github.com/hahahaday12/WinkBook/assets/101441685/58e068f3-1da5-40e3-809c-71883c02963b"><br/>

<img width="300" alt="image" src="https://github.com/hahahaday12/WinkBook/assets/101441685/cd5fe296-d09b-47ff-84c2-8525aeb5df0f">
<img width="300" alt="image" src="https://github.com/hahahaday12/WinkBook/assets/101441685/e1365745-2741-4c51-8b27-dd509d32ca58">


--------------------------------------------------------------

# == 와 ===의 차이점

## 📌 == 동등 연산자 <br/>
-> 두 값의 타입을 자동으로 변환하고, 그 후에 값의 동등성을 비교

### Ex)<br/>
5 == ‘5’ (true) <br/>
숫자 5와 문자열 ‘5’ 타입을 변환하면 값이 동일하기 때문. 자동변환 때문에 예상치 못한 결과 나옴<br/>

## 📌 === 일치 연산자 <br/>
-> 두 값의 타입과 값이 완전히 동일한지 비교.<br/>
### Ex)<br/>
5 == ‘5’ (true) <br/>
숫자와 문자열의 타입이 다르기 때문에 값의 동등성 여부 조차 비교 하지 않고 false

### ⭐ 결론 
-> === 쓰는게 더 좋다. 타입 간의 변환이 없기 때문에 명시적으로 값을 비교할 수 있으며,  더 예상 가능한 결과를 얻을 수 있기 때문 이다.

---------------------------------------------------------------

# JavaScript의 작동방식의 장단점

## 장점 
### 1. 웹브라우저에서 실행 가능
   -> 웹 브라우저 내에서 별도의 컴파일 작업 없이 사용자의 브라우저에서 동작 가능.
### 2. 동적 언어 	
     -> 변수의 타입을 미리 선언 안해도 사용가능. 이로인해 유연한 개발 가능, 빠른 프로토타이핑 가능
### 3. 간단문법	
   -> c언어와 유사. 배우기 쉽고 직관적
### 4. 이벤트기반	
   -> 이벤트 기반의 비동기 프로그래밍 지원. 웹페이지 내에서 다양한 상호작용과 비동기 작업처리 
### 5. 크로스 플랫폼	
   -> node.js 환경에서도 실행, 서버측에서도 사용
### 6. 라이브러리 와 프레임워크	
   -> 다양한 라이브러리와 프레임워크 존재. 개발 생산성 높일수 있음. 


## 단점 

### 1. 브라우저 종속성
   -> 브라우저마다 JavaScript의 실행 환경이 다를 수 있어, 크로스 브라우징 이슈가 발생	
### 2. 보안 위협 
-> 클라이언트 측 스크립트는 사용자의 브라우저에서 실행되므로 악의적인 사용자에 의해 코드가 조작될 수 있다.
### 3. 실행 속도	
   -> JavaScript는 인터프리터 언어이기 때문에 컴파일 언어보다 실행 속도가 상대적으로 느리다.
### 4. 콜백 헬
   ->  콜백 함수의 중첩이 복잡성을 증가시킬 수 있으며, 이를 "콜백 헬(callback hell)"이라고 한다.
### 5. 메모리 관리	
   ->JavaScript는 가비지 컬렉션을 통해 메모리를 관리하지만, 잘못된 메모리 관리로 인해 누수가 발생


