date-created:: [[2025-10-16]] 
date-modified::
division:: makr
stack:: JavaScript
tags:: this
type::
status:: [[ai-generated]]

- ## Summary
	- JavaScript의 `this` 키워드는 함수가 **정의**될 때가 아닌 **호출**될 때, 즉 **런타임(Runtime)**에 동적으로 결정된다.
	- 함수의 **호출 방식**이 `this`가 무엇을 참조할지 결정하는 핵심 요소다.
	- 단, **화살표 함수(Arrow Function)**는 예외적으로 자신만의 `this`를 갖지 않고, 상위 스코프(Lexical Scope)의 `this` 값을 그대로 물려받는다.
- ## Steps
	- ### **1. `this`의 기본 개념: 런타임 vs 컴파일 타임**
	  id:: 68f86531-335e-460e-b17a-b78af0b45a7a
		- **현재 JavaScript (런타임 결정)**
			- `this`의 값은 런타임에 결정된다. 즉 컨텍스트에 따라 값이 달라진다.
			- 따라서 같은 `sayHi` 함수라도 `user` 객체에서 호출하면 `this`는 `user`가 되고, `admin` 객체에서 호출하면 `this`는 `admin`이 된다.
			- ```js
			  let user = { name: "John" };
			  let admin = { name: "Admin" };
			  
			  function sayHi() {
			    // 여기서 this를 사용했다.
			    // this는 런타임에 결정되므로 호출 시점의 this가 무엇인지 확인해야 한다.
			    // 따라서 17번 행에 가서야 런타임에서 this가 실행될 것이다.
			    alert( this.name );
			  }
			  
			  // 별개의 객체에서 동일한 함수를 사용함
			  user.f = sayHi;
			  admin.f = sayHi;
			  
			  // 'this'는 '점(.) 앞의' 객체를 참조하기 때문에
			  // this 값이 달라짐
			  user.f(); // John  (this == user)
			  admin.f(); // Admin  (this == admin)
			  
			  admin['f'](); // Admin (점과 대괄호는 동일하게 동작함)
			  ```
		- **컴파일 타임 결정 (가정)**
			- `this`가 함수 정의 시점, 즉 컴파일 타임에 확정된다면, `sayHi`는 전역 스코프에 정의되었으므로 `this`는 항상 전역 객체를 참조하게 된다.
			- 컴파일 시점에서 this가 결정되다면 `this`는 전역 객체인 `window`를 참조하게 된다.
			- ```js
			  name = "Sue";
			  let user = { name: "John" };
			  let admin = { name: "Admin" };
			  
			  user.f = sayHi;
			  admin.f = sayHi;
			  
			  // 런타임 결정 (현재)
			  user.f();  // "John" (this == user)
			  admin.f(); // "Admin" (this == admin)
			  
			  // 컴파일 타임 결정 (가정)
			  user.f();  // "Sue" (this == window)
			  admin.f(); // "Sue" (this == window)
			  ```
			- 따라서 `window.name`에 이미 `Sue`를 할당했으므로 위 코드에서 `this.name`은 언제나 `Sue`이다.
		- **핵심 차이점 비교표**
			- | 구분 | 런타임 결정 (현재 JS) | 컴파일 타임 결정 (가정) |
			  |---|---|---|
			  | **결정 시점** | 함수 **호출** 시 | 함수 **정의** 시 |
			  | **`this` 값** | 호출 방식에 따라 **변함** | 정의 위치에 따라 **고정** |
			  | **유연성** | 같은 함수를 다른 객체에서 재사용 가능 | 함수가 특정 컨텍스트에 영구 바인딩 |
	- ### **2. `this` 결정 규칙 (5가지)**
		- **1. 메서드 호출**
			- `this`는 해당 메서드를 호출한 객체를 참조한다.
			- `obj.method()`에서 `this`는 `obj`다.
		- **2. 일반 함수 호출**
			- `func()` 형태로 직접 호출 시 `this`는 전역 객체(`window`) 또는 `undefined`를 참조한다.
			- **Strict Mode vs Non-strict Mode**
				- `Non-strict mode`: `this`는 전역 객체(`window`)를 참조한다.
				- `Strict mode`: `this`는 `undefined`다.
				- ```javascript
				  function test() {
				    console.log(this);
				  }
				  
				  // Non-strict mode
				  test(); // window 출력
				  
				  // Strict mode
				  "use strict";
				  test(); // undefined 출력
				  ```
		- **3. 생성자 호출**
			- `new` 키워드로 함수를 호출하면 `this`는 새로 생성되는 객체를 참조한다.
				- ```javascript
				  function User(name) {
				    // 'new' 없이 호출하면 this는 전역 객체(window)를 가리킵니다. (non-strict mode)
				    // 'new'와 함께 호출하면 this는 새로 생성된 빈 객체를 가리킵니다.
				    this.name = name;
				    this.isAdmin = false;
				  }
				  
				  // 1. 생성자 함수로 호출 (Intended way)
				  const user = new User("John");
				  
				  console.log(user.name);    // "John"
				  console.log(user.isAdmin); // false
				  console.log(user);         // { name: "John", isAdmin: false } (새로운 객체가 생성됨)
				  
				  
				  // 2. 일반 함수로 호출 (Mistake!)
				  const result = User("Admin");
				  
				  // this가 window를 가리켰으므로, 의도치 않게 전역 변수가 생성됨
				  console.log(window.name);    // "Admin"
				  console.log(window.isAdmin); // false
				  
				  // 함수가 아무것도 반환하지 않았으므로 result는 undefined
				  console.log(result); // undefined
				  ```
				- | **구분** | **생성자 함수 (The Original Way)** | **class 키워드 (The New Way)** |
				  | ---- | ---- | ---- |
				  | **핵심** | JavaScript의 근본인 **프로토타입**을 직접 다루는 방식 | 프로토타입 방식을 **클래스처럼 보이게 포장**한 문법 |
				  | **등장 시기** | JavaScript 초기부터 존재 | ES6 (2015년)에 추가됨 |
				  | **장점** | JavaScript의 동작 원리를 깊게 이해할 수 있음 | 코드가 간결하고 직관적이며, 다른 언어와 유사해 배우기 쉬움 |
				  | **단점** | 코드가 장황하고, `prototype` 개념이 낯설어 실수하기 쉬움 | 내부 동작은 여전히 프로토타입이라, 클래스만 배우면 깊은 이해가 어려울 수 있음 |
				- [[js/class]]에서 자세한 내용을 확인하라.
		- **4. 명시적 바인딩 (`call`, `apply`, `bind`)**
			- `this`의 값을 명시적으로 특정 객체로 지정할 수 있다.
		- **5. 화살표 함수**
			- 자신만의 `this`를 갖지 않으며, 정의된 위치의 **외부 스코프** `this`를 그대로 따른다.
	- ### **3. 화살표 함수의 `this`**
		- **특별한 규칙**
			- 화살표 함수는 자신만의 `this` 컨텍스트를 생성하지 않으므로, `this`를 참조하면 가장 가까운 외부 일반 함수의 `this`를 가져온다.
			- `setTimeout`과 같은 콜백 함수에서 컨텍스트를 잃지 않고 외부 `this`를 사용하고 싶을 때 매우 유용하다.
			- **유용한 경우 (setTimeout 예제)**
				- ```javascript
				  let user = {
				    firstName: "보라",
				    sayHi() {
				      // 화살표 함수는 sayHi의 this(user)를 그대로 참조
				      setTimeout(() => {
				        alert(this.firstName); // "보라"
				      }, 1000);
				    }
				  };
				  user.sayHi();
				  ```
			- **일반 함수를 사용한 경우 (문제 발생)**
				- ```javascript
				  let user2 = {
				    firstName: "보라",
				    sayHi() {
				      // setTimeout의 콜백(일반 함수)은 직접 호출되므로
				      // this는 전역 객체를 참조하게 됨
				      setTimeout(function() {
				        alert(this.firstName); // undefined
				      }, 1000);
				    }
				  };
				  user2.sayHi();
				  ```
- ## Troubleshooting
	-
- ## log
	- [[2025-10-16]] Page created.
- ### References
	-