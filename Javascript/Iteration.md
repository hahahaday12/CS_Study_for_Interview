# 객체 안의 속성과 배열의 아이템을 순회할 때 사용하는 문법

## Object method

### Object.entries()

> Object.entries() 메서드는 주어진 객체 자체의 enumerable 속성 [key, value] 쌍의 배열을 반환. (프로토타입 체인 속성 고려 X)

```javascript
const object = { 1: 'howoo', 25: 'GS', 2: 'milky', 4: 'haha' };

Object.entries(object).forEach(([key, value]) => {
	console.log(`${key}: ${value}`);
});

// Expected output:
// 1: 'howoo'
```

---

### for...in

> `for...in` 문은 상속된 enumerable 속성들을 포함하여 객체에서 문자열로 키가 지정된 모든 열거 가능한 속성에 대해 반복. (프로토타입 체인 상의 속성까지 순회)

```javascript
const object = { 1: 'howoo', 25: 'GS', 2: 'milky', 4: 'haha' };

for (const property in object) {
	console.log(`${property}: ${object[property]}`);
}

// Expected output:
// 여기서 문제
// 1. `Object.entries` 메소드와 결과값이 같을 것이다.
// 2. 아니다. 순서가 보장되어 1-25-2-4 순서가 될 것이다.
```

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

<img width="577" alt="image" src="https://github.com/1017yu/this-is-money/assets/83483378/7a88265a-7844-43fa-8a04-7ff751671883">

---

### 프로토타입 체인 속성 고려?

```javascript
function Person(name) {
	this.name = name;
}

Person.prototype.age = 26;

const heetae = new Person('heetae');

// for...in
for (const key in heetae) {
	console.log(key, heetae[key]);
}

// Object.entries()
const entries = Object.entries(heetae);
entries.forEach(([key, value]) => {
	console.log(key, value);
});
```

---

1. `for...in`

<img width="328" alt="image" src="https://github.com/1017yu/this-is-money/assets/83483378/1070c197-a125-4b29-b5e4-21dbcd47c148">

---

2. `Object.entries()`

<img width="384" alt="image" src="https://github.com/1017yu/this-is-money/assets/83483378/03e11afb-c07c-4cc8-aa02-f02d7286b56f">

---

### Object.keys()

객체의 속성 이름들을 배열로 반환하여 순회

```javascript
const object = { 1: 'howoo', 25: 'GS', 2: 'milky', 4: 'haha' };
const keys = Object.keys(object);

keys.forEach((key) => console.log(key));

// Expected output:
// 1
// 2
// 4
// 25
```

---

### Object.values()

객체의 값들을 배열로 반환하여 순회

```javascript
const object = { 1: 'howoo', 25: 'GS', 2: 'milky', 4: 'haha' };
const values = Object.values(object);

values.forEach((value) => console.log(value));

// Expected output:
// howoo
// milky
// haha
// GS
```

---

<br />
<br />
<br />
<br />

## Array Method

### for...of

배열의 각 value를 순회

```javascript
const array = ['howoo', 'GS', 'milky', 'haha'];

for (const value of array) {
	console.log(value);
}

// Expected output:
//
//
//
//
```

---

### forEach()

배열의 각 value에 대해 콜백 함수 실행

```javascript
const array = ['howoo', 'GS', 'milky', 'haha'];

array.forEach((value) => {
	console.log(value);
});

// Expected output:
// howoo
// GS
// milky
// haha
```

---

### map()

배열을 순회하며 각 value에 대해주어진 함수를 호출한 결과를 모아 새로운 배열 생성

```javascript
const array = ['howoo', 'GS', 'milky', 'haha'];

const newArray = array.map((value) => value + '25');

console.log(newArray);

// Expected output:
//
//
//
//
```

---

### filter()

주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환

```javascript
const array = ['howoo', 'GS', 'milky', 'haha'];

const newArray = array.filter((value) => value.length > 4);

console.log(newArray);

// Expected output:
// ['howoo', 'milky']
```

---

### find()

주어진 판별 함수를 만족하는 ??? 반환. 그런 요소가 없다면 `undefined`을 반환

```javascript
const array = ['howoo', 'GS', 'milky', 'haha'];

const newArray = array.find((value) => value.length === 5);

console.log(newArray);

// Expected output:
//
```

---

### some()

배열 안의 어떤 요소라도 주어진 판별 함수를 적어도 하나라도 통과하는지 테스트한다. 만약 배열에서 주어진 함수가 true을 반환하면 true를 반환하고, 그렇지 않으면 false를 반환한다. 이 메서드는 배열을 변경하지 않는다.

```javascript
const array = ['howoo', 'GS', 'milky', 'haha'];

console.log(array.some((value) => value === 'hahaha'));

// Expected output:
//
```

---

### reduce()

배열의 각 요소에 대해 주어진 리듀서 (reducer) 함수를 실행하고, 하나의 결과값을 반환한다.

```javascript
arr.reduce(callback[, initialValue])
```

> 리듀서 함수는 네 개의 인자를 가진다.

> 참고: initialValue를 제공하지 않으면, reduce()는 인덱스 1부터 시작해 콜백 함수를 실행하고 첫 번째 인덱스는 건너 뛴다. initialValue를 제공하면 인덱스 0에서 시작한다.

1. 누산기 (accumualator): 콜백의 반환값을 누적한다. 콜백의 이전 반환값 또는, 콜백의 첫 번째 호출이면서 `initialValue`를 제공한 경우에는 `initialValue`의 값이다.

2. 현재값 (currentValue): 처리할 현재 요소.
3. 현재 인덱스 (currentIndex)(optional): 처리할 현재 요소의 인덱스. initialValue를 제공한 경우 0, 아니면 1부터 시작
4. 원본 배열 (array)(optional): reduce()를 호출한 배열

- no initailValue

```javascript
[0, 1, 2, 3, 4].reduce((acc, cur) => acc + curr);

// Expected output:
// 10 (1 + 2 + 3 + 4)
```

- yes initailValue

```javascript
[0, 1, 2, 3, 4].reduce((acc, cur) => acc + curr, 10);

// Expected output:
// 10 (10 + 1 + 2 + 3 + 4)
```
