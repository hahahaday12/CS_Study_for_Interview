# JavaScript
## 자바스크립트 내장 객체를 확장하면 안 되는 이유

<br />

### 표준 내장 객체 (Standard Built-in Object)

표준 내장 객체는 자바스크립트가 기본적으로 가지고 있는 객체를 의미합니다.<br />
즉, 우리가 만든 객체가 아닌 자바스크립트가 만들어 우리에게 제공하는 객체를 말합니다.

- `Object`
- `Function`
- `Array`
- `String`
- `Boolean`
- `Number`
- `Math`
- `Date`
- `RegExp`

<br />

### 표준 내장 객체의 확장

내장되어 있는 객체 중 우리가 원하는 기능이 없을 경우, 우리는 객체를 직접 만들어 사용할 수 있습니다.<br />
그리고 이것을 `사용자 정의 객체(User Defined Object)`라고 부릅니다.

표준 내장 객체와 사용자 정의 객체를 합친 것을 `표준 내장 객체의 확장`이라고 부르는데,<br />
즉, 자바스크립트가 제공하는 내장 객체에 사용자가 원하는 기능을 추가하는 것을 의미합니다.

<br />

### 내장 객체 확장하는 방법

- `Array.prototype`

모든 Array 인스턴스에서 해당 함수를 사용할 수 있습니다.

```jsx
let arr = new Array("junehee", "haeun", "huitae", "siwoo", "jeongwoo");

function getRandomName(array) {
	let index = Math.floor(array.length * Math.random());
	return array[index];
}

console.log(getRandomName(arr));
```

```jsx
Array.prototype.random = function() {
	let index = Math.floor(this.length * Math.random());
	return this[index];
}
```

```jsx
let arr = new Array("junehee", "haeun", "huitae", "siwoo", "jeongwoo");

arr.random();
```

<br />

- `Array constructor`

Array 생성자에 직접 추가하는 방식으로 정적 함수가 됩니다.<br />
Array 인스턴스에서는 사용할 수 없고 오직 Array 생성자에서만 사용할 수 있습니다.

```jsx
Array.sayHello = function() {
	return 'Hello World';
}
```

```jsx
let arr = new Array("junehee", "haeun", "huitae", "siwoo", "jeongwoo");

arr.sayHello();    // TypeError
Array.sayHello();  // 'Hello World'
```

<br />

### 내장 객체의 확장이 안 좋은 이유

- **충돌 발생**
    
    `Array.prototype`을 확장하는 여러가지 라이브러리를 사용한다고 가정했을 때, 서로 다른 라이브러리가 이름은 같고 구현과 목적이 다른 하나의 메소드 함수를 확장해서 사용할 경우 충돌이 발생합니다.
    
- **어려운 코드 이해와 유지보수**
    
    충돌이 발생한 코드는 하나의 구현이 또 다른 구현을 덮어쓰게 되어 예상하지 못한 동작이 발생하게 됩니다. 이러한 경우에 코드를 이해하기 어렵고 유지보수 및 디버깅이 어려울 수 있습니다.
    
<br />

### 내장 객체 확장을 사용할 수 있는 경우

- `Polyfill`
    
    polyfill은 오래된 브라우저에서 지원하지 않는 최신 기능을 사용할 수 있도록 할 때 필요한 기능입니다. 
    브라우저가 다른 방식으로 동일한 기능을 구현하는 문제를 해결하는데 사용됩니다.
    특정 브라우저에서 비표준 기능을 사용하여 자바스크립트를 액세스 할 수 있는 표준 준수 방법을 제공합니다. 현대 브라우저는 대부분 표준 시맨틱에 따라 광범위한 API 세트를 구현하기 때문에 폴리 필을 사용하여 브라우저 별 구현을 처리하는 것은 오늘날 실제로 존재하지 않습니다.

<br />

### 내장 객체 확장의 대안
내장 객체를 확장하는 대신 프로젝트 전체에서 가져오고 사용할 수 있는 유틸리티 함수를 만들거나 `Object.defineProperty()` 를 사용하면 내장 객체를 수정하지 않고 다른 라이브러리나 다른 개발자와의 충돌을 방지하기 때문에 안전하며 쉬운 유지보수와 디버깅이 가능합니다.

- `Utility Function`
- `Object.defineProperty()`
    
    객체에 새로운 속성을 직접 정의하거나 이미 존재하는 속성을 수정한 후 해당 객체를 반환하는 정적 메소드
    
    ```jsx
    Object.defineProperty(obj, prop, descriptor);
    ```
    
    ```jsx
    const obj = {};
    
    Object.defineProperty(obj, 'property1', {
    	value: 100,
    	writable: false,
    })
    
    console.log(obj.property1);
    console.log(obj.writable);
    ```
    

