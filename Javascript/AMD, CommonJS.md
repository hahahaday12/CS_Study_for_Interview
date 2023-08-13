# JavaScript
### 모듈 (Module)

웹 사이트의 규모↑ 프로그래밍 소스를 관리하고 배포하는 비용↑ 레거시 코드의 의존성 파악 어려움↑<br />
따라서, JavaScript를 범용적으로 사용하기 위해서는 ‘모듈화’ 필수! (이러한 모듈화 작업 때문에 Node.js 탄생)

모듈화 시스템 등장 이전에는 브라우저에서 `<script>` 태그를 사용하여 파일 불러오는 작업 실행<br />
but 전역 스코프를 공유하는 치명적인 단점이 존재한다.

```html
<!DOCTYPE HTML>
<html lang="ko">
<head>
	<title>MODULE</title>
	<script src="a.js"></script> <!-- let number = 10 -->
	<script src="b.js"></script> <!-- let number = 20 -->
	<script>
		console.log(number); // number = 20
	</script>
</head>
</html>
```

> **모듈화(Modularization)**<br />
> 재사용 가능한 코드의 덩어리, 어떤 기능에 대한 코드 묶음 (= 하나의 파일!)

> **모듈화 3조건** : 1. 스코프 (Scope)   2. 정의 (Definition)   3. 사용 (Useage)

- **높은 재사용성** : 같은 코드의 반복성을 줄여 재활용 가능
- **쉬운 유지보수** : 모듈화가 잘 되어있을 경우 의존성을 줄일 수 있기 때문에 기능 개선 및 수정이 용이
- **네임스페이스화** : 코드의 양이 많으면 전역 스코프에 존재하는 변수명이 겹칠 가능성이 있지만 모듈로 분리시킬 경우 모듈만의 네임스페이스가 존재
- **메모리 및 네트워크 비용 절약** : 필요한 로직만 load 하여 사용하고, 한 번 load된 모듈은 웹 브라우저에 저장되기 때문에 메모리 및 네트워크 비용 절약

<br />

### 모듈 시스템 (Module System)
- `AMD` : 가장 오래된 모듈 시스템 중 하나 (RequireJS)
- `CommonJS` : Node.js 환경을 위해 만들어진 모듈 시스템
- `UMD` : AMD와 CommonJS 등 다양한 모듈 시스템을 함께 사용하기 위해 개발
- `ES Module` : ES2015(ES6)에서 도입된 모듈 시스템
    - `<script type="module">`
    - `export` , `import`

<br />

## CommonJS
JavaScript가 브라우저에 종속된 언어에서 벗어나 서버에서도 사용 가능한 언어가 되면서 Node.js 환경에서 모듈을 사용하기 위해 채택된 모듈 시스템으로, 동기적 특성을 가져 브라우저와 서버 사이드 개발에 모두 사용하기 용이얃야얃

- 내보내기 : `exports`
- 모두 내보내기 : `module.exports`
- 불러오기 : `require`

```jsx
const mod1Function = () => console.log('첫번째 모듈화!')
const mod1Function2 = () => console.log('두번째 모듈화!')

module.exports = { mod1Function, mod1Function2 }
```

```jsx
exports.mod1Function = () => console.log('첫번째 모듈화!')
exports.mod1Function2 = () => console.log('두번째 모듈화!')
```

```jsx
const mod1Function = require('./module.js')
const mod1Function2 = require('./module.js')

const testFunction = () => {
    console.log('CommonJS를 학습합니다.')
    mod1Function()
}

testFunction()
```

🎓 **Quiz!**

```jsx
let a = 1;
let b = 2;

exports.sum = function(c, d) {
	return a + b + c + d;
}
```

```jsx
let a = 3;
let b = 4;

const moduleA = require("./A");
moduleA.sum(a, b);  // ?
```

- **정답은?** `10`

<br />

### CommonJS 문제점
CommonJS의 모듈 명세는 모든 파일이 로컬 디스크에 저장되어 있어 필요할 때 바로 불러올 수 있는 상황을 전제한다. 즉, 서버 사이드 환경(Node.js)이 전제 조건으로 설정되어 있다. 하지만 이러한 방식은 필요한 모듈을 모두 내려받을 때 까지 사용 불가한 결정적인 단점을 가지고 있다.

- 해결책 : 동적으로 `<script>` 태그 삽입하는 방식 사용 (JavaScript loader가 사용하는 일반적인 방법)

브라우저에서는 서버 사이드 환경과 달리 파일 단위의 스코프가 존재하지 않는다. 또한 `<script>` 태그를 이용해 파일을 불러올 경우 순서에 따라 전역 변수가 겹치는 문제가 발생한다. 때문에 서버 모듈을 비동기적으로 클라이언트에 전송하기 위해서는 해결책이 필요!

- 해결책 :  `모듈 전송 포맷(Module Transport Format)` 추가 정의
    
    이 명세에 따라 서버 사이드에서 사용하는 모듈을 브라우저에서 사용하는 모듈과 같이 전송 포맷으로 감싸주면 비동기적으로 로드가 가능하다.

<br />

**서버 사이드에서 사용하는 모듈**

```jsx
let sum = require("./math").sum;

exports.plusTwo = function(a) {  
	return sum(a, 2);  
};
```

`plus-two.js` 에서 같은 위치에 있는 `math.js` 내의 `sum` 함수를 `require` (불러오기)

이후 `plusTwo` 라는 함수를 만들어 `exports` (내보내기)

<br />

**브라우저에서 사용하는 모듈**

```jsx
require.define({"complex-numbers/plus-two": function(require, exports) {
	let sum = require("./complex-number").sum;
	exports.plusTwo = function(a) {  
		return sum(a, 2);  
	};
}, ["complex-numbers/math"]);
```

브라우저에서는 똑같은 상황임에도 `["complex-numbers/math"]` 를 통해 먼저 로드되어야 할 모듈을 기술하고 `require.define` 안에 `plus-two` 라는 모듈을 콜백 함수 안에 정의


<br />
<br />

## AMD (Asynchronous Module Definition)

= 비동기적 모듈 선언

 CommonJS가 서버 사이드 환경에서 사용하기 좋은 반면 AMD는 필요한 파일을 네트워크를 통해 내려받아야 하는 브라우저 환경에 적합하다.

- 내보내기 : `define()`
    
    ```jsx
    define('모듈이름', ['의존성1', '의존성2'], function( 의존성1, 의존성2 ){
        // 모듈 코드
    })
    ```
    
- 불러오기 : `require()`
    
    ```jsx
    require(['모듈이름'], function(모듈) {
        // 모듈 사용
    })
    ```

<br />

### define()

브라우저 환경은 파일 스코프가 존재하지 않기 때문에 `define()` 함수로 파일 스코프 처리 (네임스페이스 역할)

`define(id?, dependencies?, factory)`

- `id` : 모듈을 식별할 때 사용하는 인수. id가 없으면 로더가 요청하는 <script> 태그의 src 값을 설정.
- `dependencies` : 정의하려는 모듈의 의존성을 나타내는 배열 (먼저 로드해야 하는 모듈)
- `factory` : 모듈이나 객체를 인스턴스화 하는 실제 구현 담당

```jsx
// define을 이용해 새로운 모듈을 불러오고, 콜백함수로 전해줌
define(['package/lib'], function (lib) {
  // 콜백함수 이용해서, 불러온 모듈 사용가능
  function foo () {
    lib.log('hello world!');
  }
  
  // 다른파일에서 foo함수를, foobar이란 이름의 모듈로 불러올 수 있게 만듬
  return {
    foobar: foo
  };
});
```

```jsx
// 위에서 선언한 모듈 불러오기
require(['package/myModule'], function (myModule) {
  myModule.foobar();
});
```

<br />

### AMD의 장점

- 브라우저와 서버 사이드 환경에서 동일한 코드로 동작 가능
- CommonJS의 모듈 전송 포맷보다 간단하고 명확
- define() 함수를 통해 파일 스코프 처리를 하기 때문에 전역 변수 문제X
- 모듈을 필요한 시점에 로드하는 Lazy-Loading(동적 로딩) 응용 가능

<br />

### UMD (Universal Module Definition)

AMD와 CommonJS 두 그룹으로 나눠지다 보니 서로 호환되지 않는 문제가 발생한하는데,

이를 해결하기 위해 나온 방법으로 AMD와 CommonJS, window에 추가하는 방식까지 모두 가능하다.

```jsx
// root: 전역범위, factory: 모듈을 선언하는 함수

(function (root, factory) {
	// AMD 방식
  if (typeof define === 'function' && define.amd) {
    define(['exports', 'b'], factory);
	// CommonJS 방식
  } else if (typeof exports === 'object' && typeof exports.nodeName !== 'string') {
    factory(exports, require('b'));
	// Browser globals (window 객체에 모듈 내보냄)
	} else {
    factory((root.commonJsStrict = {}), root.b);
  }
}(this, function (exports, b) {  // 모듈을 생성하는 익명 함수
  exports.action = function () {};
}));
```

<br />

### 지금은?

현재 브라우저는 ES6 문법에 따라 `ES Module` 사용, Node.js 환경에서는 `CommonJS`를 기반으로 사용<br />
Node.js 환경에서 `ES Module` 사용을 위해서는 `Babel` 과 같은 트랜스 컴파일러 도구를 사용해야 했지만,<br />
Node.js v13.2 부터 `ES Module` 정식 지원이 시작됨에 따라 `CommonJS`, `ES Module` 함께 사용 가능

- 사용 방법 : package.json 파일 내 ‘type’: ‘module’ 지정

```jsx
{
  "name": "node",
  "version": "1.0.0",
  "description": "",
  "main": "b.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "type": "module"  // 여기!
}
```
