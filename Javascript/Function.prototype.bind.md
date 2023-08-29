# Function.prototype.bind 란?

-> 자바스크립트에서 함수를 생성하고 이 함수의 this 값을 특정 객체로<br/>
고정 시키는 메서드.  함수를 콜백으로 사용하거나 메서드로 전달할때, <br/>
원하는 this 값 및 일부 매개변수를 미리 설정할때 사용.<br/> 

![image](https://github.com/hahahaday12/WinkBook/assets/101441685/cdcb7307-2fdd-414d-b57e-56fe4fd132c2)<br/>

## thisArg

-> 바인딩된 함수가 호출될때 대상 함수 this에 매개 변수 로 전달되는 값입니다.<br/> 
Func 함수가 엄격모드가 아닌 경우 전역 객체로 대체 null 되고 undefined 기본 값이 객체로 변환.<br/>

## Arg1, arg2..

-> 함수에 전달할 인수. 인수를 미리 설정하고 싶은 경우 해당 인수를 지정할수 있다.<br/>

# This 란?

-> this는 JavaScript에서 현재 실행 중인 코드의 컨텍스트를 가리키는 특별한키워드입니다.<br/>
->  this의 값은 실행되는 시점과 문맥에 따라 다양하게 결정됩니다.<br/> 
this의 값을 결정하는 요소

1. 함수 호출 방법: 함수가 어떻게 호출되었느냐에 따라 this의 값이 달라질 수 있습니다.<br/>
2. 호출 위치: 함수가 어떤 객체나 컨텍스트 내에서 호출되었는지에 따라 this가 가리키는 대상이 다를 수 있습니다.<br/>
3. 화살표 함수 vs 일반 함수: 화살표 함수와 일반 함수는 this의 동작 방식이 다릅니다.<br/>
4. 메서드 내부와 외부: 객체의 메서드 내부와 외부에서 this의 값이 다를 수 있습니다.<br/>


## This 예시
![image](https://github.com/hahahaday12/WinkBook/assets/101441685/dd359bdb-ff70-4c10-874d-67159ce22f08)

-> person.greet 는 person의 객체 메서드로 호출되어있기 때문에 this = person 객체 자체를 가리킨다.<br/>
-> person.greet 함수를 변수 greetFunction 의 변수에 할당하여 호출 했기때문에 this의 메서드와연결이 끊겨 전역 객체를 가리키거나 , undefined 가 될수 있다.<br/>
-> undefined 가 나올때는 엄격모드일때. ‘use strict’ 모드에서는 함수 내부의 this 는 undefined<br/>

# Bind 사용 예시
![image](https://github.com/hahahaday12/WinkBook/assets/101441685/3a3f9c47-3561-4c76-9050-75302f5df2ef)

-> bind 메서드의 첫 번째 인수는 this 값을 지정하고, 두 번째 인수부터는 해당 함수의 매개변수를 설정<br/> 
-> user.sayHello 함수 내에서 this 값을 user로, greeting 매개변수를 Hello로 전달후 새로운 함수 생성<br/>
->user.sayHello 를 greetJohn 변수에 담아 호출하면 설정한 this값과, 매개변수가 함께 사용<br/>
Consol.log = “Hello, John!”<br/>

# 어떨때 bind를 써야 할까?<br/>

## 1. 이벤트 핸들러
![image](https://github.com/hahahaday12/WinkBook/assets/101441685/1b4e7125-70ce-4835-8420-11040ef2d543)<br/>

![image](https://github.com/hahahaday12/WinkBook/assets/101441685/c79e3089-8b4f-4a3d-8ab0-c490cb9597d8)

1. button = new Button() 생성<br/>
2.  12번째 button.handleClick 의 메서드는 button. Button = this 값<br/>
3. this.handleClick = this.handleClick 에 바인딩 (this)<br/>
-> 여기서 가르키는 this = button 메서드 <br/>
4. handleClick 의 button 메서드가 바인딩이 되고  새로운 함수를 반환 한것을 this.handleClick에 정의<br/>
button 클릭후 이벤트가 일어났을때 handleClick의 접근이 가능함. 따라 콘솔창을 보면.<br/>
5. This 가 바인딩이 되었을때 button 객체 안에 handleClick 이라는 함수가 보여짐!<br/>

-> this.handleClick.bind(this);를 호출하면 원래의 handleClick 함수와 매우 유사한 새로운 함수가 반환되는데, 이 새 함수는 항상 Button 클래스의 인스턴스 (즉, this)에 연결되어 있다.<br/>

![image](https://github.com/hahahaday12/WinkBook/assets/101441685/ba516bfc-703a-45a0-8705-38862c23aeff)<br/>

= handleClick 함수에게  "너는 이 Button만 따라라!”<br/>
즉, .bind(this)를 사용하면 handleClick이 어디에서 호출되든지 그것이 'Button' 클래스에 속한 것처럼 동작하게 만드는 것.<br/>


## 2. 콜백 함수에서의 사용<br/>
![image](https://github.com/hahahaday12/WinkBook/assets/101441685/c789e18e-7e12-46af-80b7-25b05040eb82)

1. user.sayHello.bind(user)를 1초(1000밀리초) 후에 실행<br/>
2. .bind(user)는 친구를 연결해주는 역할. sayHello 함수에 user 객체를 친구로 연결해주었다.<br/>
3. 따라 콘솔창에 출력 ‘Hello, John<br/>

## 3. 클래스 메서드의 바인딩
-> 클래스의 메서드를 다른 컨텍스트에서 사용해야 할 때, bind를 사용하여 원래 클래스 인스턴스와 바인딩된 새로운 메서드를 생성할 수 있습니다. 

![image](https://github.com/hahahaday12/WinkBook/assets/101441685/db2060f7-2cd8-4853-aeb2-23193a80d92d)

1. incrementFun 실행하면 바인딩된 값이 없기 때문에 undefined
2. Counter = new Counter() 생성
3.  12번째 counter.increment 의 메서드는 counter. Counter = this 값
4. this.increment = this.increment 에 바인딩 (this)
-> 여기서 가르키는 this = couter 메서드 
5. increment 의 counter 메서드가 바인딩이 되고  새로운 함수를 반환 한것을 this.increment에 정의.
정의후 incrementFun을 실행하면 바인딩된 counter 안에 있는 count = 0 이 count++ 되어 콘솔창에 1이 뜬다.

-> Bind 메서드는 이 외에도 여러 상황에서 사용. 함수의 실행 컨텍스트와 인수를 미리 설정해 코드를 안정적으로 만든다.





   


   







