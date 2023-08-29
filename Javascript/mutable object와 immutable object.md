# [JavaScript]

## mutable object와 immutable object

### immutable object?

- 불변객체(immutable object)는 생성 후 그 상태를 바꿀 수 없는 객체

### mutable object?

- 가변객체(immutable object)는 생성 후 그 상태를 바꿀 수 있는 객체

### JavaScript에서 객체는 변경이 가능한 데이터

- JavaScript에서 불변하는 값 = 원시 데이터
  - Boolean
  - null
  - undefined
  - Number
  - String
  - Symbol  
    <br/>
- 객체데이터 = 변경가능한 값
  하지만 Immutability는 객체의 상태를 변경할 수 없어야 한다
- Javascript의 객체는 참조(reference)형태로 전달하고 전달 받는다. 객체가 참조를 통해 공유되어 있다면 그 상태가 언제든지 변경될 수 있기 때문에 문제가 될 가능성도 커지게 된다.
  객체 내부 프로퍼티를 변경할 때마다

- 불변 객체가 필요한 경우

  - 객체에 변화를 가해도 원본이 그대로 남아있어야 하는 경우  
    ex) 정보가 바뀌었으면 알림 전송하는 경우, 바뀌기 전의 정보와 바뀐 후의 정보를 보여줘야하는 경우 등

  ```javascript
  var user1 = {
    name: "Lee",
    address: {
      city: "Seoul",
    },
  };

  var user2 = user1; // 변수 user2는 객체 타입이다.

  user2.name = "Kim";

  console.log(user1.name); // Kim
  console.log(user2.name); // Kim
  ```

  객체는 값이 변경이 가능하기 때문에 user1과 user2가 모두 같은 객체를 가리킨다. 그렇기 때문에 user1을 변경하면 user2도 자연스레 변경된다

- 불변성 객체로 만드는 방법

  - 자바스크립트에서 불변 객체를 만들 수 있는 방법은 기본적으로 2가지 인데 const와 Object.freeze()를 사용하는 것이다.

  ### const

  - const 키워드는 변수를 상수로 선언할 수 있다
  - 일반적으로 상수로 선언된 변수는 값을 변경 할 수 없는 값
    > 그렇다면 상수로 선언한 객체는 불변 객체일까?
  - _**아니다**_  
    왜냐하면 const는 할당된 값이 상수가 되는 것이 아니고, 바인딩된 값이 상수가 되기 때문이다

    ```javascript
    const b = {};
    b.key = "value";

    console.log(b); // {'key': 'value'}
    ```

    - const로 선언된 객체의 속성 변경 가능하다
    - const로 선언된 객체의 속성 변경이 가능한 이유는 실제 객체가 변경되는 것은 맞지만 const로 선언한 변수와 객체 사이의 바인딩은 변경되지 않기 때문
    - 따라서 자바스크립트의 **const로 객체를 선언할 경우에 객체의 속성은 언제든지 변경이 가능**하기 때문에 **_immutable_**한 상수로 사용된다고 보기 어렵다.

    그래서 const와 같이 유용하게 사용되는 것이 Object.freeze()이다

  ### Object.freeze()

  - 자바스크립트의 Object.freeze()?

    - MDN 문서에서 "객체를 동결하기 위한 메서드"라고 설명
    - 즉, Object.freeze를 사용하면 동결된 객체를 만들 수 있고, 동결된 객체에는 속성을 추가하거나 제거하는 동작이 불가능한 Immutable한 객체를 만들 수 있는 것 -또한 Object.freeze로 동결된 객체는 프로토타입의 변경도 막아준다

      ```javascript
      let itGo = {
      	elsa = 'Princess'
      };

      Object.freeze(itGo);
      ```

    - Object.freeze를 통해 객체 동결

      ```javascript
      itGo.elsa = "Prince";

      console.log(itGo); // {elsa: "Princess"} -> Not Modified
      ```

    - itGo 객체의 속성을 변경하는 시도는 불가함 > itGo 변수에 key value를 가진 객체를 바인딩 후 _**Object.freeze(itGo)**_ 를 사용해 바인딩된 변수를 동결 객체로 만들었기 때문
      ```javascript
      itGo = {
        age: 15,
      };
      console.log(itGo); // {age: 15}
      ```
    - 위와 같이 객체의 재할당은 가능함 때문에 Object.freeze()도 불변 객체라고 할 수는 없을

    **그럼 결국 불변 객체는 어떻게 만들수 있을까?**

  ### const 와 Object.freeze()

  - const의 재할당불가 + Object.freeze()의 객체속성 변경불가

  ```javascript
  const itGo = {
    elsa = 'Princess',
  };

  Object.freeze(itGo);
  ```

  - const키워드로 바인딩 된 변수를 상수화 시킨 다음, Object.freeze()로 해당 변수를 동결 객체를 만들면 객체의 재할당과 객체의 속성 둘 다 변경불가능한 불변 객체가 된다
