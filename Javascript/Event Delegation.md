# Javascript

## Event Delegation (이벤트 위임)

### 이벤트 객체
대상에서 발생한 이벤트 정보를 담고 있는 객체

- `event.target` : 실제 이벤트가 발생한 요소
- `event.currentTarget` : 이벤트를 처리하는 요소 (현재 실행중인 handler가 할당된 요소 = `this`)

<img width="700" src="https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/116873887/60a51fbd-f8a4-4fc9-a262-14c4597d86b7">

<br /><br />

### 이벤트 버블링 (bubbling)
이벤트가 제일 깊은 곳에 있는 요소에서 시작해 부모 요소를 거슬러 올라가며 계속 발생하는 현상.<br />
가장 최상단의 조상 요소를 만날 때까지 반복되며 요소 각각에 할당된 이벤트 핸들러가 동작한다.<br />
몇 개의 이벤트를 제외한 대부분의 모든 이벤트는 버블링 된다.

- `event.stopPropagation()` : 이벤트 버블링을 중단 시키는 메소드
    
    ```jsx
    eventTarget.addEventListener('click', event => {
    	event.stopPropagation();
    })
    ```
<br />

<img width="600" src="https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/116873887/487cf5b4-1b74-40ae-8730-7aae76573625">

<br />

#### 이벤트 버블링 코드 예시
```html
<div class="one">
	<div class="two">
		<div class="three"></div>
	</div>
</div>
```

```jsx
let divs = document.querySelectorAll('div');
divs.forEach(function(div) {
	div.addEventListener('click', clickEvent);
});

function clickEvent(event) {
	console.log(event.currentTarget.className);
}
```

<br /><br />

### 이벤트 캡처링 (capturing)
이벤트가 최상위 조상에서 시작해 아래로 전파되는 현상.<br />
이벤트 캡처링에서도 `.stopPropagation()`을 사용하여 캡처링을 중단 할 수 있다.<br />
캡처링을 제어하기 위해서는 `.addEventListener()`의 세 번째 매개변수로 `capture` 옵션이 포함된 객체를 전달해야 한다.

```jsx
el.addEventListener('click', function(){ }, { capture: true })
el.addEventListener('click', function(){ }, true)
```

- `capture` 옵션의 디폴트 값은 `false` , `true`를 설정하면 버블링과 반대 방향으로 탐색

<img width="600" src="https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/116873887/3feda2d8-1121-4790-a382-bf98acab18b4">

<br />

#### 이벤트 캡처링 코드 예시
```html
<div class="one">
	<div class="two">
		<div class="three"></div>
	</div>
</div>
```

```jsx
let divs = document.querySelectorAll('div');
divs.forEach(function(div) {
	div.addEventListener('click', clickEvent, true);  // 세번째 매개변수 추가!
});

function clickEvent(event) {
	console.log(event.currentTarget.className);
}
```

<br /><br />

### 이벤트 흐름 (Flow)
이벤트가 발생하고 DOM 트리에서 이벤트가 수신되는 순서<br />
특정 요소에 이벤트가 발생하면 해당 이벤트는 아래 3단계의 흐름을 거치게 된다.

**“ 누구 먼저 실행시킬 것인가? ”**

> 1. **capturing** : window 부터 target element 까지 이벤트가 하위 요소로 전달
> 2. **target** : 이벤트가 시작된 target element 에 도달 (이벤트 handler 호출)
> 3. **bubbling** : 이벤트가 target element 부터 상위 요소로 전달

<img width="700" src="https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/116873887/7b8898d5-7af5-4e1a-a54c-c734682db302">

- 어디에서든 이벤트가 발생하면 `root` 에서 가까운 순서대로 이벤트 핸들러 실행
- 하위 요소로 내려가면서 이벤트 핸들러 실행 **(= Capture Phase)**
- 이벤트 `target`인 `<td>` 태그에 연결된 이벤트가 실행 **(= Target Phase)**
- Target Phase가 끝나면 다시 역순으로 상위 요소로 올라가며 이벤트 핸들러 실행 **(= Bubbling Phase)**

<br />

**그러면 브라우저에서는 하나의 요소마다 매번 두 번의 이벤트 핸들러가 실행되나요?**<br />
**정답은?** 선택하면 됩니다.

> 🌐 “ 개발자들아, capture 단계에서 이벤트를 발생시킬래, bubble 단계에서 발생시킬래 ?<br />일단 우리의 기본값은 bubbling이니까 capturing을 하고 싶으면 특정 코드를 추가해줘. “

<br /><br />

### 이벤트 위임 (Delegation)

여러 요소의 이벤트를 핸들링 해야 할 경우 사용<br />
공통된 조상 요소에 한 번의 이벤트 핸들러를 등록하고, 조건문 등을 통해 여러 요소를 한꺼번에 제어할 수 있는 방법

```html
<h1>오늘의 할 일</h1>
<ul class="todoList">
	<li>
		<input type="checkbox" id="todo1">
		<label for="todo1">이벤트 버블링 학습</label>
	</li>
	<li>
		<input type="checkbox" id="todo2">
		<label for="todo2">이벤트 캡쳐 학습</label>
	</li>
</ul>
```

```jsx
let inputs = document.querySelectorAll('input');
inputs.forEach(function(input) {
	input.addEventListener('click', function(event) {
		console.log('선택 완료!');
	});
});
```

<img width="800" src="https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/116873887/d2357d86-4b77-4129-a0c4-51422abc8433">

<br /><br />

**동적으로 새로운 요소를 추가해볼까요?**
```jsx
let todoList = document.querySelector('.todoList');

let li = document.createElement('li');
let input = document.createElement('input');
let label = document.createElement('label');
let labelText = document.createTextNode('이벤트 위임 학습');

input.setAttribute('type', 'checkbox');
input.setAttribute('id', 'todo3');
label.setAttribute('for', 'todo3');
label.appendChild(labelText);
li.appendChild(input);
li.appendChild(label);
todoList.appendChild(li);
```

```jsx
let inputs = document.querySelectorAll('input');
inputs.forEach(function(input) {
	input.addEventListener('click', function(event) {
		console.log('선택 완료!');
	});
});
```

<img width="800" src="https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/116873887/a9041069-55c0-4f5a-95df-9c2efd177f9c">

<br />

동적으로 추가된 요소에는 Event Handler가 작동되지 않습니다.
그래서 필요한 것이 바로 '이벤트 위임'입니다.

<br /><br />

**이벤트 위임으로 핸들러 코드 변경!**
```jsx
let todoList = document.querySelector('.todoList');
todoList.addEventListener('click', function(event) {
	console.log('선택 완료!');
});
```

<img width="800" src="https://github.com/CS-TeamStudy/CS_Study_for_Interview/assets/116873887/ddb5b726-0395-407c-a899-7efe6669565c">

<br />

동적으로 추가된 요소까지 Event Handler가 잘 작동됩니다.

<br /><br />

**또 다른 이벤트 위임 방법!**

`data-*` 커스텀 속성을 이용하여 비슷한 동작을 수행하는 요소 다루기

```html
<div id="menu">
  <button data-action="save">저장하기</button>
  <button data-action="load">불러오기</button>
  <button data-action="search">검색하기</button>
</div>
```

```jsx
const action = {
  save() {
    console.log("save!");
  },
  load() {
    console.log("load!");
  },
  search() {
    console.log("search!");
  }
};

const menu = document.querySelector("#menu");

menu.addEventListener("click", (e) => {
  if (e.target.tagName === "BUTTON") {
    action[e.target.dataset.action]();
  }
});
```

- `.dataset` : 해당하는 데이터 속성의 값을 리턴

<br /><br />

**CSS Selector를 통해 더 구체적으로 요소 타겟팅하기!**

```jsx
menu.addEventListener("click", (e) => {
  if (e.target.matches("button.active")) {
    console.log("button Active!");
  }
});
```

- `Element.matches(Selector)` : 해당 element에서 Selector 포함 여부를 boolean 값으로 리턴

<br /><br />

### 이벤트 위임의 장단점
#### 장점
- 코드의 단순화 → 메모리 사용량 감소
- 동적으로 추가, 삭제되는 요소에서도 작동 가능 → HTML 구조의 유연성
- 개발자가 의도한대로 정교한 이벤트 핸들링 가능
#### 단점
- 이벤트 버블링이 되어야만 이벤트 위임이 가능 → focus, blur 등 특정 이벤트는 버블링X
- 낮은 레벨에 할당한 핸들러에는 event.stopPropagation() 사용 불가
- 하위 요소를 많이 가진 대규모 Container에 이벤트 핸들러가 있을 경우, CPU의 작업 부하가 늘어날 수 있음
(실제로는 무시할만한 수준이므로 크게 고려하지 않음)
