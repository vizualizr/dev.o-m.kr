alias:: js/arrow function, js/화살표함수

- ## Introduction
	- A delaration of a function with bravity.
	- ```javascript
	  let func = (arg1, arg2, ...argN) => expression
	  ```
	- 지정된 매개변수를 받아 표현식으로 구한 값을 반환하는 함수를 선언한다.
	- 길게 쓰면 아래와 같다.
	- ```javaScript
	  let func = function (arg1, arg2, ...argN) = {
	  	return expression;
	  }
	  ```
	- 가장 위에 있는 기본 구문을 아래와 같이 다양한 방법으로 줄여 쓴다.
		- ```javascript
		  // 인수가 하나일 경우 괄호를 생략할 수 있다.
		  let double = n => n*2;
		  
		  // 인수가 없는 화살표 함수는 괄호를 생략할 수 있다.
		  let hello = () => alert("hello");
		  hello();
		  
		  // 함수에 분기를 추가할 수 있다.
		  let randomInt = Math.random()*2;
		  let  = (num > 0.5) ? ()=>console.log("over") : console.log("below");
		  toss();
		  ```
		- 위의 축약형은 return을 사용하지 않는다.
		- 표현식(expression)이 한 줄이므로 해당 식의 결과를 그대로 반환하기 때문이다.
	- 중괄호를 쓴 화살표 함수.
		- ```js
		  let sum = (a, b) => {  // 중괄호는 본문 여러 줄로 구성되어 있음을 알려줍니다.
		    let result = a + b;
		    return result; // 중괄호를 사용했다면, return 지시자로 결괏값을 반환해주어야 합니다.
		  };
		  
		  alert( sum(1, 2) ); // 3
		  ```
		- 중괄호를 쓴 표현식은 반드시 ==`return`으로 반환값을 명시==해야 한다.
- ### Reference
	- https://ko.javascript.info/arrow-functions-basics
	- https://javascript.info/arrow-functions-basics
- ### Log
	- [[2025-10-16]] created.