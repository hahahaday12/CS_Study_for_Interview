## 동기 vs 비동기
![](https://velog.velcdn.com/images/junsgk/post/fb571246-f623-4b8e-951d-f96cb79b5b0d/image.png)

동기와 비동기의 사전적 의미는 다음과 같다
`동기` 동시에 일어나는 
`비동기` 동시에 일어나지 않는

그러나 위 사진을 보면 특정 시점에서 동시에 여러작업이 일어나고 있는 것은 오른쪽에 있는 `Asynchronous`, `비동기`이다.

이러한 비직관적인 사전적 의미로 인해 프로그래밍에서의 `동기` `비동기` 개념이 ~~나만~~ 어렵게 느껴진다. 

`동기`라는 개념을 "요청과 결과가 동시에 일어난다" 와 같이 설명하기도 하지만 이 역시 직관적으로 받아들이기 어려운 설명이다.

따라서 동기와 비동기를 사전적 의미보다는 다음과 같이 이해하는 것이 좋다.

`동기` 답변(결과)을 기다림
`비동기` 답변(결과)을 기다리지 않음

### 동기 : 답변(결과)을 기다림
`동기`는 요청을 하면 시간이 얼마나 걸리던지 결과를 기다리고, 결과를 받고나서야 다음 작업을 진행할 수 있다.

동기방식은 설계가 간단하고 직관적이지만 결과가 주어질 때까지 아무것도 못하고 대기를하는 `blocking`이 발생한다.

```js
// 코드 한줄 한줄을 요청이라 생각하고 해당 줄이 실행되는 것을 결과라고 생각할 수 있다.
const 동기함수 = function () {
  console.log('작업 시작');
  for (let index = 0; index < 10000; index++) {
    console.log('무거운작업');
  }
  console.log('작업 끝');
};

동기함수();

// 작업 시작
// 무거운작업 x 10000
// 작업 끝
// undefined
```

### 비동기 : 답변(결과)을 기다리지 않음
`비동기` 처리에 대해 알아보기에 앞서 비동기 처리는 왜 필요할까?

만약 웹페이지가 `동기적`으로만 작동한다면 서버로 부터 데이터를 받아오는 동안 해당 웹페이지는 blocking된 상태로 정지될 것이다.

`비통기`는 요청을 하면 결과를 내주지 않더라도 다음 작업을 진행할 수 있다.

답을 즉시 처리 하지 않아도, 그 대기 시간 동안 또다른 요청이 가능한 방식이므로 `non-blocking` 이다.

```js
const 비동기함수 = async function () {
  try {
    const response = await fetch(
      'https://jsonplaceholder.typicode.com/todos/1'
    );
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.log(error);
  }
};

console.log('작업 시작');
비동기함수();
console.log('작업 끝');


// 작업 시작
// 작업 끝
// undefined
// {userId: 1, id: 1, title: 'delectus aut autem', completed: false}
```

자바스크립트는 싱글스레드로 프로그램이 동작한다. 그런데 비동기 처리방식은 필연적으로 하나 이상의 스레드가 필요하다.
이를 위해 웹브라우저는 자바스크립트 엔진과 더불어 Web API에서 이러한 비동기적 작업들을 처리하게 된다.

그러면 `callback`, `promise`, `async/await` 은 뭐냐?
답변(결과)가 언제 올 지 모르는 `비동기`작업을 `동기적`으로 작업하기 위한 기술들이다. 즉 비동기 작업을 보다 효율적이고 가독성 있게 다루기 위한 방법들이다.