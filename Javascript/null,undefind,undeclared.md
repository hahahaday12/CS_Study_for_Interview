# [JavaScript]

## null,undefind and undeclared

- null,undefind and undeclared은 모두 **변수에 값이 없다는 점을 나타낸다**, 하지만 셋의 의미는 각각 다르다

  ### undefined(미정의 변수)? 타입이 결정되지 않은 변수

  - **접근 가능한 스코프**에 변수가 선언되었으나 현재 아무런 값도 할당되지 않은 상태

    > ### 💡 스코프(Scope)란?
    >
    > **선언된 변수에 대해서 접근할 수 있는 유효한 범위를 의미**
    >
    > ##### 만약, 변수가 해당 스코프에 존재하지 않다면 사용할 수 없다. 그리고 계층적인 구조를 가지기 때문에 하위 스코프는 상위 스코프에 접근할 수 있지만, 상위 스코프는 하위 스코프에 접근할 수 없다.

    ```javascript
    let 감자여친; // <- 타입이 정의 되어 있지 않음
    console.log(감자여친); //undefined
    console.log(typeof 감자여친); //undefined
    ```

  - 선언된 변수는 암묵적으로 undefined로 초기화 됨
    - _변수 선언에 의해 확보된 메모리 공간_ 을 처음 할당이 이뤄질 떄까지 빈상태(대부분 비어있지 않고 쓰레기 값이 들어있음)로 두지 않고 **JS가 undefined로 초기화**하기에 변수를 선언한 이후 값을 할당하지 않으면 초기화된 undefined가 반환되는 것이다  
      <br/>
  - undefined는 개발자가 의도적으로 할당하기 위한 값이 아니라 자바스크립트 엔진이 변수를 초기화 할때 사용하는 값
    - 자바스크립트 엔진이 변수를 초기화하는데 사용하는 undefind를 의도적으로 변수에 할당한다면 **_undefind의 취지와 어긋나고 혼란을 야기하므로 권장하지 않음_** > **_null을 사용한다_**

  ### null? 타입은 객체이고 비어있는 변수

  - null은 의도적으로 변수에 null을 할당하여 값이 없다는 것을 나타낸다.
  - **_Null이 할당된 변수의 타입을 확인해 보면 object인 것을 알 수 있다_**

    ```javascript
    let 밀키남친 = null;
    console.log(밀키남친); // null
    console.log(typeof 밀키남친); //object
    ```

  - 변수에 null을 할당하는 것은 변수가 이전에 참조하던 값을 더 이상 참조하지 않겠다는 의미

    - 이는 이전에 할당되어 있던 값에 대한 참조를 명시적으로 제거하는 것을 의미하며
    - JS는 누구도 참조하지 않는 공간에 대해 **가비지컬렉션을 수행함**(더 이상 사용하지 않는 메모리를 자동으로 정리/메모리누수 방지)

  - typeof 에서 null
    - **null은 객체이고 참조 자료형**이다

  ### undefined == null, undefined === null

  ```javascript
  console.log(undefined == null); //true
  console.log(undefined === null); //false
  ```

  - **비교연산자(==)는 자료형이 다르면 자료형을 강제로 맞춰서 비교하는 연산자**
  - Undefined와 null은 자료형이 다르니 강제로 맞춰서 값을 비교하면 둘다 값이 없으니 true 반환
  - **_하지만 === 연산자를 이용하면 자료형까지 비교하므로 false 반환_**
  - null은 의도적으로 빈 값이 들어간 object이기 때문

  ### undelared(미선언 변수)? 접근 가능한 스코프에 변수 선언조차 되어있지 않은 상태

  - 접근 가능한 스코프에 변수 선언조차 되어있지 않은 상태로 타입은 undefined 상태이다

    ```javascript
    // 변수 선언이 되어있지 않음
    console.log(내남친); //ReferenceError: b is not defined <오류>
    console.log(typeof 내남친); //undefined
    ```

    <br/><br/><br/>
