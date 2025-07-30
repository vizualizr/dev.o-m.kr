date-created:: [[2025-07-28]]
date-modified::
division::
stack::
tags:: [[javascript]] 
type::
public:: true
alias:: 접근자 함수

- ## Summary
	- 객체의 속성에 접근할 수 있도록 하는 함수이다. 일반적으로 getter와 setter가 있다.
- ## Steps
- ## Troubleshooting
	- #### Syntax
		- “In addition, accessor functions that spread over multiple lines require body braces ({}) and a return statement (e.g., for the class attribute), while simple, single-line functions don’t need them (e.g., for the width attribute). These rules are summarized in figure 3.19.” ([Meeks, 2024, p. 90](zotero://select/library/items/VHTGXJRT))
		- 여러 줄에 걸쳐 작성한 접근자 함수는 꺾쇠({})로 감사야 하며 *return* 구문을 포함해야 한다.
		- 반변 한줄로 된 간략한 함수는 위 두 가지가 없어도 된다.
		- 또한 매개변수(parameter)가 두 개 이상일 경우 해당하는 매개변수를 괄호로 묶어야 한다.
			- ```js
			  selection
			    .attr("y", (d, i) => (barHeight + 5) * i)
			  ```
	-
- ## log
	- [[2025-07-28]]
- ### References
	-