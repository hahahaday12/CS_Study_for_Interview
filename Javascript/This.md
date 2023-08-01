# [JavaScript] this

![image](https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/125563995/fc3ad8f1-9f07-4803-a528-775927fc2bad)
  
## what is this?  누가 나를 불렀어?
  - this란? JavaScript **예약어**

    - this는 자바스크립트 엔진에 의해 암묵적으로 생성된다.

    - this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수(self-reference variable)이다.

    - this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.

    - this는 코드 어디서든 참조할 수 있다.
    **하지만 this는 객체의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수이므로 일반적으로 객체의 메서드 내부 또는 생성자 함수 내부에서만 의미**가 있다

    - 함수를 호출하면 인자와 **this가 암묵적으로 함수 내부에 전달**된다

    - 함수 내부에서 인자를 지역 변수처럼 사용할 수 있는 것처럼, this도 지역 변수처럼 사용할 수 있다

    - 단, this가 가리키는 값, 즉 **this 바인딩은 함수 호출 방식에 의해 동적으로 결정**된다 (크게 전역에서 사용할 때와 함수안에서 사용할 때로 나눌 수 있다)

      ``` javascript
      const foo = function () {
        console.log(this);
      };

      // 1. 함수 호출
      foo(); // window
      // window.foo();

      // 2. 메소드 호출
      const obj = { foo: foo };
      obj.foo(); // obj

      // 3. 생성자 함수 호출
      const instance = new foo(); // instance

      // 4. apply/call/bind 호출
      const bar = { name: 'bar' };
      foo.call(bar);   // bar
      foo.apply(bar);  // bar
      foo.bind(bar)(); // bar
      ```
<br/><br/>

## 함수 호출 방식에 따른 this 바인딩

  - 전역객체

    - 전역객체? 전역객체(Global Object)는 모든 객체의 유일한 최상위 객체를 의미하며 일반적으로 Browser-side에서는 window, Server-side(Node.js)에서는 global 객체를 의미함

    - ~~전역객체는 전역 스코프(Global Scope)를 갖는 전역변수(Global variable)를 프로퍼티로 소유한다~~ 글로벌 영역에 선언한 함수는 전역객체의 프로퍼티로 접근할 수 있는 전역 변수의 메소드이다

    - **_기본적으로 this는 전역객체(Global object)에 바인딩된다_**

    - 다만, strict mode(엄격 모드)에서는 조금 다름,
     **함수 내의 this에 디폴트 바인딩이 없기 때문에 undefined**

 

## this가 전역객체(Global object)에 바인딩 되는 경우  

  - 전역함수 

    ---
  - 내부함수
    - 내부함수는 일반 함수, 메소드, 콜백함수 어디에서 선언되었든 관게없이 this는 전역객체를 바인딩

    ```javascript
    function foo() {
      console.log("foo's this: ",  this);  // window
      function bar() {
        console.log("bar's this: ", this); // window
      }
      bar();
    }
    foo();
    ```
    ---
  - 메소드의 내부함수 (not method)
    ```javascript
    const value = 1;

    const obj = {
      value: 100,
      foo: function() {
        console.log("foo's this: ",  this);  // obj
        console.log("foo's this.value: ",  this.value); // 100
        ------------------------------ 메소드
        function bar() {
          console.log("bar's this: ",  this); // window
          console.log("bar's this.value: ", this.value); // 1
        }
        bar();
        ------------------------------ 메소드의 내부함수
      }
    };

    obj.foo();
    ``` 
    ---
  - 콜백함수
    ```javascript
    const value = 1;

    const obj = {
      value: 100,
      foo: function() {
        setTimeout(function() {
          console.log("callback's this: ",  this);  // window
          console.log("callback's this.value: ",  this.value); // 1
        }, 100);
      }
    };

    obj.foo();
    ```
    
## this가 전역객체(Global object)에 바인딩 되지 않는 경우

- 메소드 안에서 쓴 this
  - 함수가 객체의 프로퍼티 값이면 메소드로서 호출된다. 이때 메소드 내부의 this는 해당 메소드를 소유한 객체, **즉 해당 메소드를 호출한 객체에 바인딩**

    ```javascript
    const hee = {
      name: 'Lee',
      sayName: function() {
        console.log(this.name);
      }
    }

    const hee2 = {
      name: 'Kim'
    }

    obj2.sayName = obj1.sayName;

    obj1.sayName(); // Lee
    obj2.sayName(); //Kim
    ```
    <img width="716" alt="image" src="https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/125563995/68d27f70-c1ac-4746-ae90-fc602771b3aa">

    ```javascript
    const hee = {
      name: 'Yoo',
      sayName: function() {
        console.log(this.name);
      }
    }
    hee.sayName(); // YOO

    const hee2 = hee.sayName;
    hee2(); //window
    ```
  ---
  <br/>
- 이벤트 핸들러 안에서 쓴 this
  - 이벤트 핸들러에서 this는 이벤트를 받는 HTML 요소를 가리킴 
    ```javascript
    var btn = document.querySelector('#btn')
    btn.addEventListener('click', function () {
      console.log(this); //#btn
    });
    ```
  ---
  <br/>
- 생성자 안에서 쓴 this
  - 생성자 함수가 생성하는 객체로 this가 바인딩 
    ```javascript
    function Person(name) {
      this.name = name;
    }
 
    var kim = new Person('kim');
    var lee = new Person('lee');

    console.log(kim.name); //kim
    console.log(lee.name); //lee
    ```
  ---
  <br/>
- 명시적 바인딩을 한 this
  - call() / apply()
    ```javascript
    let person1 = {
      name: 'Jo'
    };

    let person2 = {
      name: 'Kim',
      study: function() {
        console.log(this.name + '이/가 공부를 하고 있습니다.');
      }
    };

    person2.study(); // Kim이/가 공부를 하고 있습니다.

    // call()
    person2.study.call(person1); // Jo이/가 공부를 하고 있습니다.
    ```
    - call()
      > func.call(thisArg[, arg1[, arg2[, ...]]])
      - thisArg: func 호출에 제공되는 this의 값
      - arg1, arg2, ...: func이 호출되어야 하는 인수

    - apply()
      > fun.apply(thisArg, [argsArray])
      - thisArg: func 호출에 제공되는 this의 값
      - argsArray: func이 호출되어야 하는 인수를 지정하는 **배열,유사 배열** 객체
  
  - bind()
    ```javascript
    let person1 = {
      name: 'Jo'
    };

    let person2 = {
      name: 'Kim',
      study: function() {
        console.log(this.name + '이/가 공부를 하고 있습니다.');
      }
    };

    person2.study(); // Kim이/가 공부를 하고 있습니다.

    // bind()
    let student = person2.study.bind(person1);
    
    student(); // Jo이/가 공부를 하고 있습니다.
    
    ```
    - bind()
      > func.bind(thisArg[, arg1[, arg2[, ...]]])
      - thisArg: 바인딩 함수가 타겟 함수의 this에 전달하는 값
      - arg1, arg2, ...: func이 호출되어야 하는 인수
      - **_bind()는 call(), apply()와 같이 함수가 가리키고 있는 this를 바꾸지만 호출되지는 않음, 따라서 변수를 할당하여 호출하는 형태로 사용한다_**
