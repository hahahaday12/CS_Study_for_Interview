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

그러면 브라우저에서는 하나의 요소마다 매번 두 번의 이벤트 핸들러가 실행되나요?<br />
**정답은?** 선택하면 됩니다.

> 🌐 “ 개발자들아, capture 단계에서 이벤트를 발생시킬래, bubble 단계에서 발생시킬래 ?<br />일단 우리의 기본값은 bubbling이니까 capturing을 하고 싶으면 특정 코드를 추가해줘. “

