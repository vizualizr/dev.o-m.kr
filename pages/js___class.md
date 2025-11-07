date-created:: [[2025-10-17]] 
date-modified::
division:: [[makr]]
stack:: 
tags:: class, 생성자함수, prototype, 객체지향
type::

- ## Summary
	- JavaScript의 생성자 함수는 **클래스 문법이 없던 시절의 객체 생성 방식**이다.
	- ES6에서 도입된 `class` 키워드는 JavaScript의 근본 동작(프로토타입)을 바꾼 것이 아니라, 기존의 생성자 함수 방식을 더 편리하고 직관적으로 사용할 수 있도록 포장한 **문법적 설탕(Syntactic Sugar)**이다.
	- 즉, `class`는 생성자 함수의 **개선판**이며, ==내부적으로는 여전히 프로토타입 기반으로 동작==한다.
- ## Steps
	- ### **1. 태초의 방식: 프로토타입과 생성자 함수 (The Original Way)**
		- JavaScript는 Java, C++과 달리 **클래스 기반(Class-based)이 아닌 프로토타입 기반(Prototype-based)** 언어로 탄생했다.
		- 별도의 `class`(설계도) 개념 없이, '원본 객체(prototype)'를 만들어두고 이를 복제하여 새 객체를 생성하는 방식이었다.
		- **생성자 함수**는 이 '원본 복제 및 초기화' 과정을 자동화하는 역할을 수행했다.
		- **예시 코드**
			- `prototype`을 직접 다루어야 해서 코드가 직관적이지 않고 복잡했다.
			- ```javascript
			  // 생성자 함수
			  function Person(name) {
			    this.name = name;
			  }
			  
			  // 원본(prototype)에 메서드 추가
			  Person.prototype.sayHi = function() {
			    console.log("Hi, I'm " + this.name);
			  };
			  
			  // 'new'를 통해 객체 생성
			  const john = new Person("John");
			  john.sayHi(); // Hi, I'm John
			  ```
	- ### **2. 개선판: `class` 키워드의 등장 (The New Way - ES6)**
		- 프로토타입 방식이 다른 언어 개발자들에게 낯설고 불편하다는 의견을 반영하여, 2015년 ES6에서 `class` 문법이 도입되었다.
		- `class`는 새로운 개념이 아니라, 기존의 프로토타입 방식을 더 익숙하고 깔끔하게 포장한 **문법적 설탕**에 해당한다.
		- 내부 동작 원리는 프로토타입 방식과 완전히 동일하다.
		- **예시 코드**
			- 코드가 훨씬 간결하고, 객체 생성을 위한 설계도라는 의도가 명확하게 드러난다.
			- ```javascript
			  class Person {
			    // 생성자 함수 역할을 하는 constructor
			    constructor(name) {
			      this.name = name;
			    }
			  
			    // 메서드를 직관적으로 정의 (내부적으로는 prototype에 추가됨)
			    sayHi() {
			      console.log("Hi, I'm " + this.name);
			    }
			  }
			  
			  const john = new Person("John");
			  john.sayHi(); // Hi, I'm John
			  ```
	- ### **3. 핵심 비교**
		- | 구분 | 생성자 함수 (The Original Way) | `class` 키워드 (The New Way) |
		  |---|---|---|
		  | **핵심** | JavaScript의 근본인 **프로토타입**을 직접 다루는 방식이다. | 프로토타입 방식을 **클래스처럼 보이게 포장**한 문법이다. |
		  | **등장 시기**| JavaScript 초기부터 존재했다. | ES6 (2015년)에 추가되었다. |
		  | **장점** | JavaScript의 동작 원리를 깊게 이해할 수 있다. | 코드가 간결하고 직관적이며, 배우기 쉽다. |
		  | **단점** | 코드가 장황하고, `prototype` 개념이 낯설어 실수하기 쉽다. | 내부 동작은 프로토타입이라, 깊은 이해가 부족할 수 있다. |
	- ## Troubleshooting
		-
	- ## log
		- [[2025-10-17]] Page created.
	- ### References
		- <!-- end list -->