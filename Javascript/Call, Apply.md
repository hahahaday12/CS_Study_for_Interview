# [JavaScript]

## call,apply

- call()와 apply() 함수들은 bind() 함수처럼 만약 객체1에서 객체2의 함수를 빌려 쓰고 싶을 때 사용함

  ### call,apply의 차이점

  - 매개변수 처리 방법에서 차이가 있음
  - 첫 번째 인자가 this로 지정할 객체라면, 두 번째 인자부터는 함수에 넘겨줄 매개변수를 지정할 수 있음
  - call()는 여러 인자를 나열해서 받고 apply()는 여러 인자를 한 배열에 받음

    ```javascript
    const bank = {
      deposit: function (amount) {
        this.money += amount;
      },
      deposits: function (amountOne, amountTwo) {
        this.money += amountOne + amountTwo;
      },
    };

    const john = {
      money: 0,
    };

    bank.deposit.call(john, 100); 
    console.log(john.money); //100

    bank.deposits.apply(john, [200, 300]);
    console.log(john.money); //600
    ```

  - call()의 경우 call(john, 인자1, 인자2, 인자3)

    ```javascript
    const dog = {
      age: 12,
    };
    function printDogAge(name, location) {
      console.log(this.age, name, location);
    }
    printDogAge.call(dog, "mike", "seoul"); // 12, mike, seoul
    ```

  - apply()의 경우 apply(john. [인자1, 인자2, 인자3])

    ```javascript
    const dog = {
      age: 12,
    };
    function printDogAge(name, location) {
      console.log(this.age, name, location);
    }
    printDogAge.apply(dog, ["mike", "seoul"]); // 12, mike, seoul
    ```

- 왜 call 과 apply를 나눠서 사용하는가?

  - 배열 매개변수를 받는 게 좋은 상황  
    예시) `Math.min()` 을 사용할때

    > Math.min()은 인자로 넘긴 값 중 제일 작은 값을 리턴해주는 함수

    ```javascript
    const minValue = Math.min(12, 200);
    console.log(minValue); //12
    ```

    - 만약 우리가 배열에서 제일 작은 값을 알고 싶다면 어떻게 해야할까?

    ```javascript
    const arr = [1, 23, 4, 55, 231];
    const minValue = Math.min(...arr); // spread 연산자를 사용하지 않은 경우 (arr)일때는 NaN
    console.log(minValue); // 1
    ```

    - 하지만 배열 그대로 넣고 싶다면? 이때 **_apply_** 를 사용해줄수 있다

    ```javascript
    const arr = [1, 23, 4, 55, 231];
    const minValue = Math.min.apply(null, arr);
    console.log(minValue); //1
    ```

    - this로 지정할 객체가 없으므로 null로 지정하고, 두 번째 인자로 배열을 넣어주면 된다

  ### 정리

  - call, apply 메소드 모두 명시적 this 바인딩을 할때 사용함
  - call, apply 메소드는 메서드의 호출 주체인 함수를 즉시 실행함
  - apply 메소드는 첫번째 인자 이후의 인자들을 배열로 받음
