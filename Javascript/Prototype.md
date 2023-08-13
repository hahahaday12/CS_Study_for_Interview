# 자바스크립트 프로토타입

- Java, C++과 같은 class 기반 객체지향 프로그래밍 언어와 달리 자바스크립트는 프로토타입 기반 객체지향 프로그래밍 언어이다.
- Prototype 개념을 class 개념으로 이해하면 안된다.

  - 자바스크립트에서는 class가 없다.
  - 자바스크립트에서는 '복사'를 통한 상속이 아닌 prototype link를 통한 상속.

# 상속이란?

- 자기 자신의 객체에는 없지만 상위 객체의 속성 또는 메서드를 사용하는 것

```js
const cat = {
  legs: 4,
  isCute: true,
  meow: function () {
    console.log('meow');
  },
};
cat.hasOwnProperty('isCute'); // true
// cat에는 hasOwnProperty라는 메서드가 없지만 사용이 가능함
```
<img width="304" alt="image-11" src="https://github.com/howooking/CS_Study_for_Interview/assets/87072568/26a60d4e-df4a-43b6-b2b7-3733c2232fc9">

# \_\_proto\_\_ vs prototype

### \_\_proto\_\_

- 모든 객체는 생성이 되면 \_\_proto\_\_가 자동으로 생성된다.
<img width="584" alt="image-12" src="https://github.com/howooking/CS_Study_for_Interview/assets/87072568/a158f7d4-17d9-45e7-bdf3-6808b56cfd2c">
<img width="601" alt="image-14" src="https://github.com/howooking/CS_Study_for_Interview/assets/87072568/1d455a5f-ed0b-4c3a-90ec-203feae9b0f2">

- \_\_proto\_\_는 상속의 기능을 구현하기 위해 상위 객체의 주소정보를 가지고 있는 속성

```js
const cat = {
  legs: 4,
  isCute: true,
  meow: function () {
    console.log('meow');
  },
};

const howoo = {
  color: 'gold',
};

// cat객체와 howoo객체는 서로 연관이 없는 객체이다.

cat.__proto__ === Object.prototype; // true
howoo.__proto__ === Object.prototype; // true
```
<img width="531" alt="image-17" src="https://github.com/howooking/CS_Study_for_Interview/assets/87072568/20ed08f3-f21e-43aa-a20d-d5b5505c0ec3">

```js
howoo.__proto__ = cat; // howoo의 __proto__를 cat객체에 연결

howoo.__proto__ === cat; // true
cat.__proto__ === Object.prototype; // true
howoo.__proto__.__proto__ === Object.prototype; // true

// prototype chain
howoo.meow(); // meow
howoo.hasOwnProperyty('color'); // true
howoo.like; // undefined
```
<img width="805" alt="image-16" src="https://github.com/howooking/CS_Study_for_Interview/assets/87072568/80150d99-24b3-4c94-aacc-2b322f6457f4">

### prototype

- 생성자 함수에만 존재하는 속성
- 함수가 생성자로 사용될 때 이 함수를 통해 생성될 객체의 부모 역할을 하는 객체(프로토타입 객체)를 말한다.

```js
function Cat(name) {
  this.name = name;
  this.leg = 4;
  this.isCute = true;
  this.salute = function () {
    console.log(`meow! my name is ${this.name}`);
  };
}

const howoo = new Cat('howoo');
const mongo = new Cat('mango');
howoo.salute(); // meow! my name is howoo
mango.salute(); // meow! my name is mango

```
<img width="692" alt="image-23" src="https://github.com/howooking/CS_Study_for_Interview/assets/87072568/8f7c7c90-c3c1-48db-b5b5-0b64f2e4a508">

```js
howoo.__proto__ === Cat.prototype; // true
// 일반적인 객체였다면 howoo.__proto__는 Object.prototype을 가리키겠지만 생성자 함수로 생성된 객체는 생성자함수.prototype을 가리킨다.

Cat.__proto__ === Function.prototype; // true
Cat.prototype.constructor === Cat; // true
Cat.__proto__ === Function.prototype; // true
Cat.prototype.__proto__ === Object.prototype; // true
Function.prototype.__proto__ === Object.prototype; // true

howoo.hasOwnProperty('color'); // false

mango.salute === howoo.salute; // false
//Cat 생성자 함수를 통해 생성된 howoo.salute 과 mango.salute 은 동일한 로직을 가지고 있지만 다른 각자 다른 메모리 공간을 차지하고 있음
```

- 생성자함수.prototpye을 통해 공통의 로직을 prototype 객체에 넣을 수 있음

```js
Cat.prototype.jump = function () {
  console.log(`${this.name} jumps!`);
};

howoo.jump(); // howoo jumps!
mango.jump(); // mango jumps!
howoo.jump === mango.jump; //true
```

<img width="687" alt="image-24" src="https://github.com/howooking/CS_Study_for_Interview/assets/87072568/604211c1-f34d-4fd0-afea-72e0eba42c3d">

- 생성자함수.[property | function] 할 경우

```js
Cat.eat = function () {
  console.log(`${this.name} eating!`);
};
howoo.eat(); // howoo.eat is not a function
mango.eat(); // mango.eat is not a function
Cat.eat.call(howoo); // howoo eating!
```

<img width="683" alt="image-26" src="https://github.com/howooking/CS_Study_for_Interview/assets/87072568/59ade5f0-6532-432c-9c8a-694f3d503a63">

- class 문법

```js
class Cat {
  leg = 4;
  isCute = true;
  static eat = function () {
    console.log(`${this.name} eating!`);
  };

  constructor(name) {
    this.name = name;
    this.salute = function () {
      console.log(`meow! my name is ${this.name}`);
    };
  }

  jump() {
    console.log(`${this.name} jumps!`);
  }
}

const howoo = new Cat('howoo');
```
