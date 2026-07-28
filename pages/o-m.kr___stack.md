date-created:: [[2026-07-03]]
date-updated:: [[2026-07-11]] 
alias:: o-m.kr/stacks
tags::
ai-sourced:: 
division::
stack::
type::
public:: true

- ## Summary
	- The layers for all the required features.
- ## Steps
	- Core stacks.
		- [[astro]] for web framework
		- [[d3.js]] for contents
		- [[GSAP]] and [[lenis]] for animation
	- Stacks for [[visual semantics]]
		- [[tailwindcss]] for styling
		- UI & Asset libraries
			- [[DaisyUI]] for [[UI component]] / tailwind dependent
			- [[lucide icons]] for icons / framework independent
	- updated on [[2026-07-11]]
- ## Troubleshooting
	- #2026-07-03 [[FlyonUI]]에서 [[DaisyUI]]로 변경함.
		- 나중에 GSAP가 자바스크립트 애니메이션을 제어할 때 flyonUI의 애니메이션을 제어하는 JS가 DOM을 제어하는 과정에서 GSAP와 충돌할 수 있다. DaisyUI에는 JS가 전혀 없다. DOM 제어 충돌과 같은 문제를 걱정할 필요가 없다.
		- [[astro]]의 기본 철학인 NO js에 부합한다.
		- DaisyUI에서는 CSS 파일 하나로 색상 관리를 통합할 수 있디. 별도로 테마를 주입하지 않고 차트 내부요소의 색상을 Tailwind 클래스나 저 CSS 변수(`var(--color-primary)`)로 그대로 가져다 쓸 수 있다.
	- [[2026-07-24]] svelte도 붙여야 하나? #스벨트
		- 복잡한 사용자 입력/상태 관리가 필요하거나, (예: 사용자가 여러 개의 필터 버튼을 누르거나, 슬라이더를 조작해 데이터셋 전체를 실시간으로 바꿀 때)
		- 하나의 기사 안에 독립적인 차트 컴포넌트가 10개 이상 재사용될 때
		- 위와 같은 상황이 오면 Astro의 아일랜드 기능(@astrojs/svelte)으로 필요한 부분에만 스벨트를 부분 도입을 추천한다.
- ## log
	- [[2026-07-03]] Page created.
- ### References
	-