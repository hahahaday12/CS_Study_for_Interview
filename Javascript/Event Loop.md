## 📌 사전지식

> **JavaScript 동작 원리**<br />
자바스크립트는 싱글 스레드 기반으로 하나의 콜 스택(Call Stack)과 하나의 메인 스레드를 가집니다.
싱글 스레드는 한 번에 하나의 일(명령)만 처리할 수 있다는 의미이며,
그렇기 때문에 자바스크립트는 동기식(Synchronous) 언어라고 할 수 있습니다.
> 

> **JavaScript 런타임**<br />
자바스크립트는 엔진에 하나의 메모리 힙과 하나의 콜 스택이 존재하는 싱글 스레드 기반의 동기식 언어이므로, 다른 작업을 실행하려면 현재 작업이 끝나기를 기다려야 하는 문제점이 발생합니다.
이것을 해결하기 위해 오래 걸리는 일을 백그라운드에서 처리하고, 간단하게 처리할 수 있는 작업만 콜 스택에서 수행하는 것을 런타임(Runtime)이라고 합니다.
> 

> **JavaScript 런타임 환경**<br />
Memory Heap, Call Stack, Web APIs, Task Queue(Cb Queue), Event Loop
> 

<img width="800" src="https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/116873887/9943f02b-2ca5-4ec0-b684-3e27868d7198" />

<br />

## 콜 스택 (Call Stack)

콜 스택은 함수의 호출을 저장하는 자료구조입니다. 어떠한 함수를 호출했을 경우 스택에 쌓이고, 또 다른 함수를 호출하면 그 다음 스택에 쌓이면서 가장 위에 쌓인 함수를 가장 먼저 처리합니다. (Last In First Out, LIFO)

<br />

<img width="" src="https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/116873887/842b7de1-643c-4ce9-afa6-7b0592a3b34c" />


- `예제 코드`
    
    ```jsx
    const func1 = () => {
        func2();
        console.log('첫 번째 함수입니다.');
    }
    
    const func2 = () => {
        func3();
        console.log('두 번째 함수입니다.');
    }
    const func3 = () => {
        console.log('세 번째 함수입니다.');
    }
    
    func1();
    ```
    
<img width="" src="https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/116873887/41bf044a-ba17-463a-afcc-bbd55f946d70" />

- `func1` 함수를 가장 먼저 호출하기 때문에 `call stack` 에는 `func1` 이 쌓여 있습니다.
- `func1` 함수 내에서 `func2` 함수를 호출하므로 `call stack` 에 `func2` 함수가 추가로 쌓입니다.
- `func2` 함수 내에서 `func3` 함수를 호출하므로 `call stack` 에 `func3` 함수가 마지막으로 쌓입니다.
- `call stack` 에서는 가장 위에 놓인 함수를 가장 먼저 처리하므로 `func3 → func2 → func1` 순서대로 출력합니다.

<br /><br />

## 이벤트 루프 (Event Loop)

이벤트 루프는 Call Stack과 Task Queue를 감시하여, Call Stack이 모두 비워지면 Task Queue에 존재하는 함수를 하나씩 Call Stack으로 옮기는 역할을 합니다. 태스크가 들어오기를 기다렸다가 태스크가 들어오면 이를 처리하고, 처리할 태스크가 없을 경우에는 잠드는 자바스크립트 내 단일 스레드 루프입니다.

<br />

<img width="" src="https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/116873887/93e3e0a2-b678-4915-919e-1fd46ae64e11" />

- `예제코드`
    
    ```jsx
    function main() {
      console.log('First');
      setTimeout(
        function display() { console.log('Second'); }
      , 0);
    	console.log('Third');
    }
    
    main();
    ```

<img width="" src="https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/116873887/1238bf73-9d0c-4db8-aab2-b578649de8da" />

<br />

1. `main` 함수에 대한 호출이 먼저 call stack 에 추가(push)됩니다. 그런 다음 브라우저는 `main` 함수의 첫 번째 명령문인 `console.log('First')` 를 call stack에 추가합니다. call stack은 LIFO 형태로 이루어지기 때문에 나중에 들어온 `console.log('First')`가 먼저 실행되어 브라우저 콘솔에 출력된 뒤, `call stack`에서 제거(pop)됩니다.
2. 다음 명령문인 `setTimeout` 이 call stack에 추가 및 실행 되면서 브라우저가 제공하는 `timer Web API`를 호출한 후에 call stack 에서 제거됩니다.
3. `console.log('Third')`는 브라우저에서 `timer`가 실행되는 동안 스택에 추가가 되며,  setTimeout 함수에 전달한 0ms 의 시간만큼 지연된 이후 task queue에 콜백이 추가됩니다.
4. `main` 함수에서 마지막 명령문이 실행된 후 `main` 함수가 call stack에서 제거되어 call stack이 비어있게 됩니다. **이벤트 루프**는 call stack이 비어있는 것을 확인하고 task queue를 살펴본 뒤, 콜백 함수를 발견하여 call stack에 콜백 함수를 추가합니다.
    - 브라우저가 대기열인 task queue 에서 call stack으로 메시지를 추가하려면 먼저 call stack이 비워져있어야 합니다. 바로 이것 때문에 `setTimeout` 에서 제공된 지연시간이 0ms임에도 다른 모든 것들이 실행이 완려될 때까지 기다려야 하는 이유입니다.
5. 이제 콜백 함수가 call stack으로 추가되어 `console.log('Second')` 가 실행됩니다.

<br /><br />

## 태스크 큐 (Task Queue, Callback Queue)

이벤트가 발생했을 때 실행해야 하는 콜백 함수가 저장됩니다. 태스크 큐는 마이크로 태스크 큐와 매크로 태스크 큐로 나뉘어지는데, 사용하는 API에 따라 구분하여 사용할 수 있습니다.

- **Micro Task Queue (Event Queue)**
    - process.nextTick, Promises, queueMicrotask(f), MutationObserver…
- **Macro Task Queue (Job Queue)**
    - requestAnimationFrame, I/O, UI rendering, setTimeout, setInterval, setImmediate…

<img width="" src="https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/116873887/53a0c306-29e2-43db-85b2-c87413b2b68f" />

<br /><br />

## 콜 스택과 태스크 큐의 차이점

- **콜 스택**은 자바스크립트 코드가 실행되는 함수가 저장됩니다.
- **태스크 큐**는 이벤트가 발생했을 때 실행되는 콜백 함수가 저장됩니다.
- **태스크 큐**에 저장된 콜백 함수는 **콜 스택**이 비어있을 때 **이벤트 루프**에 의해서 **콜 스택**에 추가됩니다.
- 만약 **콜 스택**이 비어있지 않다면 **태스크 큐**에 저장된 콜백 함수는 실행되지 않습니다.

<br /><br />

## 그래도 이해가 안 된다면 아래 영상을 보시길...

[어쨋든 이벤트 루프가 무엇입니까? | Philip Roberts | JSConfEU](https://youtu.be/8aGhZQkoFbQ?si=ZIb5Zt0mzJvMWpOa)
