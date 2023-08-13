# Javascript

![자바스크립트 객체의 3가지 분류](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a6993a74-299f-4c70-836e-490dfb65e3eb/Untitled.png)

자바스크립트 객체의 3가지 분류

## 네이티브 객체 (Native Objects)

자바스크립트 언어 규약, 즉 ECMAScript 명세에 정의된 객체로 애플리케이션 전역의 공통 기능을 제공하며, 애플리케이션 환경에 관계없이 언제나 사용할 수 있다. 각 네이티브 객체는 각자의 프로퍼티와 메소드를 가진다.
간단하게 설명하면 실행 환경에 종속되지 않고 우리가 예상한 방향대로 실행할 수 있는 객체를 말한다.

`= Global Objects , Built-In Objects`

*전역 객체(Global Object)와는 다른 의미이므로 혼동하지 않도록 주의!*

### 네이티브 객체 종류

- Object() 생성자 함수
    
    ```jsx
    const obj = new Object();
    const obj = {};
    ```
    
- Function 객체
    
    ```jsx
    const plus = new Function('a', 'b', 'return a + b');
    plus(2, 3); // 5
    ```
    
- Boolean : 원시 타입 boolean을 위한 Wrapper Object
    
    ```jsx
    const foo = new Boolean(true);     // true
    const foo = new Boolean('false');  // true
    const foo = new Boolean(false);    // false
    const foo = new Boolean(0);        // false
    
    const junehee = new Boolean(false);
    if (junehee) {
    	// 이 코드는 실행될까요? 안 될까요?
    }
    ```
    
- Array, String, Number, Boolean
- Symbol, Map, Set, RegExp, Date, Math, Promise, Error, JSON, Proxy…

<br />

### 원시 타입과 Wrapper Object

<aside>
📌 **원시타입 (Primitive Type)**
String, Number, BigInt, Boolean, Undefined, Symbol, Null

</aside>

네이티브 객체는 각자의 프로퍼티와 메소드를 가진다. 정적(static) 프로퍼티와 메소드는 인스턴스를 생성하지 않아도 사용할 수 있고 prototype에 속해있는 메소드는 해당 prototype을 상속받은 인스턴스가 있어야지만 사용할 수 있다.

**그. 러. 나**

그동안 string, number 타입 또한 메서드를 가지며 마치 객체인 것 처럼 사용했듯이 원시 타입 값에 대해 표준 내장 객체의 메소드를 호출하면 정상적으로 작동하게 된다.

```jsx
const str = 'javascript';
const res = str.toUpperCase();
console.log(res); // 'JAVASCRIPT'
```

왜냐하면 원시 타입 값에 대해 표준 내장 객체의 메소드를 호출할 때, 원시 타입 값은 연관된 객체(= `wrapper object`)로 일시 변환되기 때문이다. 그리고 메소드 호출이 종료되면 다시 원시 타입 값으로 복귀하게 된다. 

<br />

### Wrapper Object

래퍼 객체란 원시 타입의 값을 감싸는 형태의 객체이다.

원시 타입인 `number`, `string`, `boolean`, `symbol` 에 각각 대응하는 `Number`, `String`, `Boolean`, `Symbol`이 제공되며 이들은 객체형(참조형) 데이터 타입이다.

```jsx
const str = 'javascript';
console.log(str.length);  // 10
console.log(str.charAt(0));  // 'j'
```

```jsx
const str = 'javascript';
console.log(str.length);  // new String(str).length
```

‘javascript’ 라는 문자열 값을 가지고 있는 str의 데이터 타입은 string이다. 즉 원시형 데이터 타입이기 때문에 원래라면 객체처럼 메소드를 가질 수 없다. 하지만 자바스크립트는 `number`, `string`, `boolean`, `symbol` 에 대해서 일시적으로 ‘객체화’ 되는 것을 허용하며 그 순간에는 `number`, `string`, `boolean`, `symbol` 조차 객체처러 메서드를 사용할 수 있다.

```jsx
const n = 100;
const num = new Number(n);

console.log(n == num);   // true
console.log(n === num);  // false

console.log(typeof n);    // number
console.log(typeof num);  // object
```

원시 타입과 래퍼 객체는 동등 연산자(`==`)로는 구분할 수 없지만 엄격 동등 연산자(`===`)로는 구분할 수 있다.

<br />

## 호스트 객체 (Host Objects)

호스트 환경(실행 환경)에서 제공하는 객체를 말하며 운영체제(OS)와 브라우저에 따라 제공 객체가 달라진다. 예를 들어 브라우저에서 동작하는 환경과 브라우저 외부에서 동작하는 환경의 자바스크립트(Node.js)는 다른 호스트 객체를 사용할 수 있다. 브라우저에서 동작하는 환경의 호스트 객체는 전역 객체인 window, DOM, BOM, XmlHttpRequest 등이 있으며, 네이티브 객체가 아닌 객체는 모두 호스트 객체이다.

아주 대표적인 예로 `console.log()`!

<br />

### 1️⃣  전역 객체 (Global Object)

모든 객체의 유일한 최상위 객체를 의미한다. `(Global Objects !== Global Object)`

- 브라우저에서는 `window`
- 서버 사이드 환경(Node.js)에서는 `global` 객체

<br />

### 2️⃣  BOM (Browser Object Model)

브라우저 객체 모델은 브라우저의 탭 또는 브라우저의 창 모델을 생성한다.

- 최상위 객체 `window` : 현재 브라우저 창 또는 탭을 표현하는 객체
- 최상위 객체의 자식 객체들은 브라우저의 다른 기능을 표현
- 자식 객체들은 Standard Built-in Objects가 구성된 후에 구성된다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dc3dc7ff-a953-4d4c-aa72-625fe4b4c8ab/Untitled.png)

<br />

### 3️⃣  DOM (Document Object Model)

문서 객체 모델은 현재 웹 페이지의 모델을 생성한다.

- 최상위 객체 `document` : 전체 문서를 표현하며
- 최상위 객체의 자식 객체들은 문서의 다른 요소들을 표현
- BOM과 마찬가지로 Standard Built-in Objects가 구성된 후에 구성된다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/05f284c7-4cdc-4105-bffa-648de9db86c5/Untitled.png)

<br />

## 결론은

- 환경에 관계없이 사용할 수 있는 네이티브 객체를 파악하고 있어야 한다.
- 자바스크립트가 실행되는 환경에서 사용할 수 있는 객체를 파악하고 사용할 수 있어야 한다.
