# 익명함수 vs 선언적 함수

> 자바스크립는 매우 유연한 언어이다. 다른 언어들과 다르게 다양한 방법으로 함수를 선언하고 사용할 수 있다.

### 익명함수

- 함수의 이름을 명시하지 않고 변수에 담아 사용하거나 변수에 담지 않고 사용한다.

```js
let 동물소리 = function () {
  console.log('야옹');
};
동물소리 = function () {
  console.log('멍멍');
};
동물소리 = function () {
  console.log('어흥');
};
동물소리(); // 어흥
```

### 선언적 함수

- 선언적 함수는 전체 코드를 읽기 전에 호이스팅되어 선언한 순서대로 만들어진다.

```js
동물소리2(); // ?

function 동물소리2() {
  console.log('야옹');
}
function 동물소리2() {
  console.log('멍멍');
}
function 동물소리2() {
  console.log('어흥');
}
동물소리2(); // 어흥
```

- 자바스크립트에서는 선언적으로 생성된 함수를 재선언할 수 있다.

- 익명 함수와 선언적 함수를 같이 사용하다 보면 코드 예측이 어려워진다.

```js
함수(); // 선언적함수가 호이스팅 되어 실행된다.

함수 = function () {
  // 선언적함수를 덮어씀
  console.log('익명');
};

function 함수() {
  // 호이스팅
  console.log('선언적');
}

함수(); // 익명
```

- 결론: 선언적 함수 사용을 지양하자

# 익명 함수를 사용하는 이유?

> 재사용이 필요없는 함수라면 이름을 붙힐 필요가 없다.

```js
// 콜백함수
const numbers = [1, 2, 3, 4];
const double = numbers.map(function doubleFunction(num) {
  return num * 2;
});

// vs

const numbers = [1, 2, 3, 4];
const double = numbers.map(function (num) {
  return num * 2;
});

// 즉시실행 함수
(function () {
  console.log('진행시켜');
})(); // 진행시켜

// Closure
function createCounter() {
  let count = 0;
  return function () {
    return ++count;
  };
}
const counter = createCounter();
counter(); // 1
counter(); // 2
counter(); // 3
```
