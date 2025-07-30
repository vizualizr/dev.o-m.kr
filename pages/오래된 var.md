- [오래된 var](https://ko.javascript.info/var)
- |구분|`var`|`let`|
  |--|--|--|
  |스코프|함수(전역[^1]) |블록|
  |중복 선언|가능|불가능|
  |끌어올리기[^2]|끌어올림|끌어올리지 않음|
- ## Footnotes
	- [^1]: 코드 블록을 무시하기 때문에 함수가 아닌 블록 안에서 작성하면 전역 변수가 된다.
		- ```js
		  for (var i = 0; i < 10; i++) {
		    // ...
		  }
		  
		  alert(i); 
		  // 10, 반복문이 종료되었지만 'i'는 전역 변수이므로
		  // 여전히 접근할 수 있다.
		  // 반면 let으로 i를 선언해다면 
		  // 5번 줄은 `i`는 선언되지 않은 변수라며 에러를 전달한다.
		  ```
	- var는 선언된 변수의 스코프를 함수로 제한한다. 때문에 아래와 같이 함수 밖에서 참조하면 해당 변수를 선언하지 않았다는 에러를 전달한다.
		- ```js
		  function sayHi() {
		    if (true) {
		      var phrase = "Hello";
		    }
		    alert(phrase); // 할당된 값을 출력한다.
		  }
		  
		  sayHi();
		  alert(phrase); // 에러 값을 지정하지 않음
		  ```
	- [^2]: `var`로 선언한 함수는 해당 스코프를 실행할 때 처리된다. 함수 블록 안에 있다면 함수를 실행할 때, 전역에서 선언했다면 스크립트가 시작할 때 처리한다. 때문에 아래처럼 변수 선언이 아래에 있어도 함수를 실행할 때  해당 구문을 함수에서 가장 위로 끌어올려(hoisting) 처리한다.
		- ```js
		  function sayHi() {
		    phrase = "Hello";
		    alert(phrase);
		    // phrase 변수 선언이 값 할당보다 나중이지만
		    // 끌어올려 처리하므로
		    // 오류 없이 실행한다.
		    var phrase;
		  }
		  sayHi();
		  ```
		- 단 할당에는 끌어올림이 없다. 그래서 선언과 할당이 병합된 코드는 나누어 실행한다.
		- ```js
		  function sayHi() {
		    alert(phrase);
		  	// 선언과 할당을 한 구문에 넣었다.
		    var phrase = "Hello";
		  }
		  
		  sayHi();
		  ```
		- 위 코드는 아래 코드와 동일하게 실행한다.
		- ```js
		  function sayHi() {
		    var phrase; // 선언은 함수를 시작할 때 처리하지만
		    // 할당된 값이 없으니 아래처럼 undefined를 반환하고
		    alert(phrase); // undefined
		    // 처리 순서가 아래에 도달한 후에 값을 할당한다.
		    phrase = "Hello";
		  }
		  
		  sayHi();
		  ```
		- 여기서 문제가 생기는데 전역 변수의 이름과 겹치지 않는 로컬 변수를 쓰고 메모리에서 버리려면 어떻게 해야하나라는 문제가 생긴다 .그래서 IIFE, 즉시 실행 함수 표현식(immediately-invoked function expressions)을 고안한다. 코드는 아래와 같다
		- ```js
		  (function() {
		  	let message = "Hello";
		  	alert(message); // Hello
		    // message는 익명함수의 로컬 변수이므로 해당 함수를 실행 완료하면 사라진다.
		    // 하지만 가독성이 나쁘기 쓰지 말도록 하자.
		  })();
		  ```