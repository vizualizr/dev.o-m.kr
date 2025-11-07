date-created:: [[2025-10-17]]
date-modified:: [[2025-10-20]] 
division:: [[makr]]
stack:: frontend
tags:: 클로저, 함수, 스코프, class, 개념정리
status:: [[ai-proofed]] 
type::
alias:: js/closure

- ## Summary
	- 클로저(closure)란 열린 함수(open function)가 해당 함수의 결괏값을 바꿀 수 있는 외부 변수를 참조할 경우 [[자바스크립트 엔진]] 해당 변수에 대한 참조를 메모리에 유지하는 동작을 일컫는다.
		- 이때 열린 함수 그리고 이 함수가 참조하는 외부 변수를 같은 스코프에서 선언하는 함수를 외부함수(outer/enclosing function)라 한다.
		- 외부함수 안에서 존재하는 열린 함수를 내부함수(innter/nested function)라 한다.
		- 열린 함수란 해당 함수 밖에 값을 참조하는 함수이다. 이 변수로 인해 함수의 결괏값이 달라지지 않아도 마찬가지로 열린 함수라 한다.
	- 이로써 함수가 값을 결정할 때 필요한 변수가 해당 함수 밖에 있을 때에도 참조할 수 있기 때문에 결과적으로 외부함수가 **클래스의 인스턴스와 유사하게 비공개 상태(private state)를 갖는 독립적인 객체처럼** 동작하게 만든다.