## Callback 함수란?

하나의 함수 안에 매개변수(parameter)로 들어가는 또 다른 함수입니다.<br />
자바스크립트의 비동기 처리 방식의 문제점을 해결하기 위해 함수가 특정 시점에서 호출되도록 사용합니다.

- **예시**
    
    ```jsx
    function func1 (callback) {
    	callback();
    }
    
    function callback() {
    	console.log("callback 이다");
    }
    
    func1(callback);
    
    // callback 이다
    ```

<br /><br />

## Promise란?

자바스크립트의 **비동기 처리**를 위해 사용되는 객체로서,
정해진 기능을 수행한 이후 성공과 실패에 따라 결과값을 나타냅니다.

<br />

## Promise를 사용하는 이유

동기 처리를 비동기 처리하면서 예측 불가능한 결과를 핸들링 하기 위해 많은 이벤트과 콜백 함수 남용

👉 **프로미스 사용으로 콜백 지옥을 벗어나 효율적인 코드 작성 가능이 가능합니다.**<br />
👉 **비동기 처리 시점을 명확하게 표현할 수 있습니다.**

<br />

## Promise 생성 방식 (a.k.a Producer)

- 일반 함수

```jsx
const promise = new Promise(function(resolve, reject) {
		// 실행 함수 (executor)
});
```

- 화살표 함수

```jsx
const promise = new Promise((resolve, reject) => {
		// 실행 함수 (executor)
});
```

프로미스는 Class이기 때문에 new 생성자를 통해 인스턴스화 하여 사용할 수 있습니다.<br />
프로미스 생성자 함수는 비동기 처리를 위한 콜백 함수를 인자로 가지며,<br />
해당 콜백 함수는 다시 `resolve` 와  `reject` 를 가지게 됩니다.<br /><br />

`resolve` 와 `reject` 는 자바스크립트가 제공하는 기본 콜백 함수입니다.<br />
때문에 별도의 함수를 작성하지 않아도 되지만 `executor`(실행 함수)에서 둘 중 하나는 무조건 호출해야 합니다.<br />
유의할 점은 `reject` 함수를 실행할 때 `new Error` 생성자를 함께 사용해주어야 한다는 점입니다.

```jsx
const promise = new Promise((resolve, reject) => {
  let success = "성공했어요!";
  resolve(success);
});
```

```jsx
const promise = new Promise((resolve, reject) => {
  let fail = "실패했어요.";
  reject(new Error(fail));
});
```
<br />

## Promise 작동 방식

프로미스를 사용할 때 가장 중요한 개념 중 하나는 **상태(state)**입니다.<br />
상태(state)는 프로미스의 처리 과정으로 총 4가지 종류가 있습니다.

- **pending (대기)** : 비동기 처리가 아직 수행되지 않은 상태
- **fulfilled (성공)** : 비동기 처리가 수행되어 결과를 반환한 상태
- **rejected (실패)** : 비동기 처리가 수행됐지만 실패하거나 오류가 발생한 상태
- *settled (성공 또는 실패) : 비동기 처리가 수행된 상태 (성공 혹은 실패)*

`new Promise` 생성자가 반환하는 promise 인스턴스의 state(상태)는 기본적으로 **pending(대기)**입니다.<br />
즉 Promise 메소드를 호출하는 순간에 **pending(대기)** 상태로 시작합니다.<br />
그리고, executor(실행 함수)가 실행된 이후 **resolve**가 호출되면  **fulfilled(성공)**으로 바뀌게 됩니다.<br />
그러나 **reject**가 호출되면 **rejected(실패)** 상태가 됩니다.

<br />

## Promise 후속 처리 메소드 (a.k.a Consumers)

### .then()

Promise의 resolve 함수가 실행될 경우 실행되는 메소드입니다.<br />
resolve가 호출 됐으므로 해당 Promise의 state(상태)는 fulfilled(성공) 상태로 변하게 되며,<br />
.then() 메소드는 Promise의 executor(실행 함수) 내에서 resolve 함수에 넘겨준 값을 value로 가지게 됩니다.

```jsx
const promise = new Promise((resolve, reject) => {
  let success = "성공했어요!";
  resolve(success);
});

promise.then(value => {
  console.log(value);     // 성공했어요!
});
```

반면에, Promise 내에서 reject 함수에 넘겨준 값은 .then() 메소드로 실행되지 않습니다.

```jsx
const promise = new Promise((resolve, reject) => {
  let fail = "실패했어요.";
  reject(new Error(fail));
});

promise.then(value => {
  console.log(value);
});
```

### .catch()

Promise의 reject 함수가 실행될 경우 실행되는 메소드입니다.<br />
reject가 호출 됐으므로 해당 Promise의 state(상태)는 rejected(실패) 상태로 변하게 되며,<br />
.catch() 메소드는 Promise의 executor(실행 함수) 내에서 reject 함수에 생성된 error를 받게 됩니다.

```jsx
const promise = new Promise((resolve, reject) => {
  let fail = "실패했어요.";
  reject(new Error(fail));
});

promise.catch(error => {
console.log(error);     // Error: 실패했어요.
});
```

### .finally()

Promise의 결과와 관계없이 Promise 실행이 완료되면 무조건 실행되는 메소드입니다.

```jsx
const promise = new Promise((resolve, reject) => {
  let success = "성공했어요!";
  resolve(success);
});

promise.finally(() => {
  console.log('상관 없어요~');     // 상관 없어요~
});
```

.finally() 메소드는 자동으로 다음 핸들러에 결과와 에러를 전달하기 때문에<br />
메소드 체이닝을 통해 then과, catch를 활용할 수 있습니다.

```jsx
const promise = new Promise((resolve, reject) => {
  let success = "성공했어요!";
  resolve(success);
});

promise
   .finally(() => { console.log('상관 없어요~'); })
   .then(value => { console.log(value); });

// 상관 없어요~
// 성공했어요!
```

```jsx
const promise = new Promise((resolve, reject) => {
  let fail = "실패했어요.";
  reject(new Error(fail));
});

promise
   .finally(() => { console.log('상관 없어요~'); })
   .catch(error => { console.log(error); });

// 상관 없어요 ~
// Error: 실패했어요.
```

<br />

## Promise 정적 메소드

### .all()

여러 개의 Promise를 비동기적으로 실행하여 처리하는 메소드<br />
Promise로 이루어진 배열을 매개변수로 가지며, 실행된 Promise의 결과값을 담은 배열을 반환한다.<br />
Promise.all()을 통해 실행된 Promise들 중 하나라도 reject(거부)되면, 모든 Promise가 전부를 reject 됩니다.

```jsx
let promise = Promise.all( [...promises...] );
```

```jsx
let p1 = new Promise((resolve, reject) => {
  setTimeout(() => resolve('1'), 1000);
});

let p2 = new Promise((resolve, reject) => {
  setTimeout(() => resolve('22'), 2000);
});

let p3 = new Promise((resolve, reject) => {
  setTimeout(() => resolve('333'), 3000);
});

let p4 = new Promise((resolve, reject) => {
  setTimeout(() => resolve('4444'), 4000);
});

Promise
	.all([p1, p2, p3, p4])
	.then(value => {
	  console.log(value);
	});

// (4) ["1", "22", "333", "4444"]
```

```jsx
Promise
	.all([
	  new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
	  new Promise((resolve, reject) => setTimeout(() => reject(new Error("에러 발생!")), 2000)),
	  new Promise((resolve, reject) => setTimeout(() => resolve(3), 3000))
])
	.catch(alert);
```

<aside>
🚫 Error: 에러 발생!

</aside>

### .race()

여러 개의 Promise를 비동기적으로 실행하여 처리하는 메소드
가장 빨리 처리된 Promise의 결과 또는 에러를 반환하며, 다른 Promise가 rejected(실패) 되더라도 error를 무시한다.

```jsx
let promise = Promise.race( [...promises...] );
```

```jsx
let p1 = new Promise((resolve, reject) => {
  setTimeout(() => resolve('1'), 1000);
});

let p2 = new Promise((resolve, reject) => {
  setTimeout(() => resolve('22'), 2000);
});

let p3 = new Promise((resolve, reject) => {
  setTimeout(() => resolve('333'), 3000);
});

let p4 = new Promise((resolve, reject) => {
  setTimeout(() => resolve('4444'), 4000);
});

Promise
	.race([p1, p2, p3, p4])
	.then(value => {
	  console.log(value);
	});

// 1
```

```jsx
Promise
	.race([
	  new Promise((resolve, reject) => setTimeout(() => resolve(1), 3000)),
	  new Promise((resolve, reject) => setTimeout(() => reject(new Error("에러 발생!")), 5000)),
	  new Promise((resolve, reject) => setTimeout(() => resolve(3), 1000))
])
	.then(alert);
```

<aside>
⚠️ 3

</aside>
