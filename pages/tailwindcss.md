date-created:: [[2025-07-23]]
date-updated:: [[2026-07-17]] 
division:: [[frontend]] 
stack::
tags::
type:: 
public:: true
alias:: tailwindCSS, TailwindCSS, Tailwind CSS, tailwind css, tailwind CSS

- ## Summary
	- 테일윈드CSS의 목표는 CSS파일 사용을 최소화하는 것이다. 때문에 기능 클래스를 HTML 파일에 바로 기입하는 것을 권장한다.
- ## Steps
	- ### color
		- #### CSS 변수(CSS custom property)
			- CSS에서 변수를 쓸 수 있다. `:root`는 이 선언한 변수의 스코프가 이 HTML의 최상단임을 나타낸다.
			- ```css
			  :root {
			    --primary-color: #004b73; /* --이름: 값; 형태로 선언 */
			    --main-padding: 16px;
			  }
			  ```
			- 선언한 뒤에는 아래처럼 불러와서 쓴다
			- ```css
			  button {
			    background-color: var(--primary-color); /* #004b73이 적용됨 */
			    padding: var(--main-padding);           /* 16px이 적용됨 */
			  }
			  ```
			- 번들러는 테일윈드 유틸리티 클래스로 선언된 구문을 CSS 변수 호출문으로 변경된 CSS 클래스로 바꿔주는 역할만 한다.
			- 반면 테일윈드는 HTML나 CSS에 `bg-primary`, `text-primary`처럼 기능 클래스로 작성한 구문을 해석해서 실제 CSS로 바꿔주는 번역기이다.
			- 즉 개발 환경에서는 테일윈드CSS에서 정의한 클래스로 적어두면 번들러는 이 구문이 실제 의미하는 CSS 파일을 생성하는 역할을 한다. 이때 CSS 구문 작성의 효율성을 높이기 위해 CSS 변수를 쓴다.
		- TODO https://tailwindcss.com/docs/colors/ [[2026-07-20]]
	- ### js 통합
		-
- ## Troubleshooting
	- `@apply` 구문의 사용.
		- TODO [Reusing Styles - Tailwind CSS](https://v3.tailwindcss.com/docs/reusing-styles) [[2026-07-20]]
			- 일단 이걸 다시 읽어야 한다.
- ## log
	- [[2025-07-23]] Page Created.
	- [[2025-07-30]] changed the structure
- ### References
	- [[prototyping d3.js and tailwindcss with Vite]]
	- [[prototyping with TailwindCSS CLI]]
	- [[css/layouts]]