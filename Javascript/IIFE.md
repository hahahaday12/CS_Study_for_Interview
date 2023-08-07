# Javascript

## IIFE

아래의 코드 중 즉시 호출 함수로 동작하는 코드는 몇 번일까요?

```

1. function foo(){
   // 함수 내부 로직
   }();

2. const foo = () => {
   // 함수 내부 로직
   }();

3. (function foo() {
   // 함수 내부 로직
   })();

4. (function foo(){
   // 함수 내부 로직
   }());

5. function foo() {
   // 함수 내부 로직
   }
   foo();

```

---

![image](https://github.com/FC-MINI-4/attendance-front/assets/83483378/89465cfd-da8f-46ca-9b6d-b2319bce0adc)

<blockquote>

**IIFE(즉시 호출 함수 표현식)** 은 주로 이름 충돌 최소화 및 private 변수 생성에 사용되는

자바스크립트 디자인 패턴 이다.

</blockquote>

IIFE의 일반적인 형식은 전체 함수를 그룹화하는 연산자(괄호 집합)로 묶고 익명 상태로 두는 것이다. 끝에있는 추가 괄호()가 즉시 호출한다.

```
(function() {
    // 함수 내용
    const siwoo = 'GS25';
    return siwoo
})();

```
<img width="227" alt="image" src="https://github.com/FC-MINI-4/attendance-front/assets/83483378/29f067d6-6a96-44aa-97d3-d63d92c7d4d7">

<br />

---


### IIFE의 다양한 사용법

1. 변수 지정

    함수 표현식은 값으로 평가되기에 IIFE를 변수에 저장할 수 있다.



```
const convenience = (function() {
    const siwoo = 'GS25';
    return siwoo
})();

convenience; 
```
<img width="284" alt="image" src="https://github.com/FC-MINI-4/attendance-front/assets/83483378/26b64689-da82-459e-b1bb-b171ffbe7a36">

---

2. 괄호 생략

    IIFE를 변수에 할당하는 경우 둘러싸는 괄호를 생략 할 수 있다.

```
const convenience = function() {
    const siwoo = 'GS25';
    alert(siwoo);
}();
```
<img width="432" alt="image" src="https://github.com/FC-MINI-4/attendance-front/assets/83483378/ac7db9af-6870-480c-9645-ef0ab6e6a260">

<br />

---

3. 괄호를 사용하지 않고, 다른 방식으로 IIFE 선언하기

    느낌표를 함수 앞에 추가하여 인터프리터가 다음을 표현식으로 인지하게 할수 있다.


```
!function() {
    const siwoo = 'GS25';
    alert(siwoo);
}();
```

<img width="679" alt="image" src="https://github.com/FC-MINI-4/attendance-front/assets/83483378/1f70e21d-1659-4fb5-8ff1-afbc4cd240fc">


---


### IIFE를 사용하는 이유는 무엇인가?

1. 캡슐화: IIFE는 함수 내에서 선언된 변수들이 함수 스코프 내에서 유지한다. 이로 인해 함수 내부의 변수들이 전역 스코프를 오염시키지 않는다. 

2. 네임 스페이스:  IIFE는 전역 스코프를 사용하지 않고 함수 내부에서 변수를 선언하므로, 전역 네임스페이스를 오염시키지 않고 코드를 구성할 수 있다. 이는 여러 라이브러리나 다른 코드와 상호작용할 때 충돌을 방지하는 데 도움이 된다.

3. 즉시 실행: IIFE는 함수를 정의한 즉시에 실행되므로, 특정 초기화 코드나 한 번만 실행되어야 하는 코드를 깔끔하게 처리할 수 있다. 특히 초기화 작업을 수행하거나, 어떤 값들을 설정하거나, 초기 설정을 단 한 번만 수행해야 할 때 유용하다.
