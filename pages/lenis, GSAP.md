item-type:: [[software]]
outcome::
host::
status:: [[ai-proofed]] 
date-of-installation::
date-of-update::

- ## Introduction
	- 스크롤을 입력 받아 상호작용을 구성하기 위한 기반 지식을 정리한다.
	- 이를 위해 웹 환경에서 lenis, GSAP 조합을 사용한다.
- ## Steps
	- ### basics
		- 브라우저의 스크롤 처리를 먼저 이해해야 lenis와 GSAP가 어떻게 여기에 개입하는지 알 수 있다.
			- 브라우저의 스크롤 처리 로직
			  logseq.order-list-type:: number
				- 스크롤 이벤트가 발생하면 `wheel`, `scroll` 이벤트를 브라우저에 전달한다.
				  logseq.order-list-type:: number
				- 사용자 입력을 기준으로 스크롤 거리, 즉 화면 상의 이동 거리를 브라우저에 다시 전달하면 화면을 즉시 해당 거리만큼 이동한다.
				  logseq.order-list-type:: number
					- 주로 픽셀 단위이며 이동 사이 속도, 거리의 보간에 개발자가 개입할 수 없어 스크롤 이동이 순간이동처럼 단절되어 보일 수 있다. (브라우저에서 기초적인 보간만을 수행한다)
					  logseq.order-list-type:: number
			- 스크롤 처리에서 지연이 발생하는 원인
			  logseq.order-list-type:: number
				- 브라우저는 메인 스레드와 합성 스레드가 서로 페이지에서 필요한 연산을 분담해 처리한다.
				  logseq.order-list-type:: number
					- 메인 스레드는 연산 담당한다. 자바스크립트 연산, HTML 파싱 등을 처리한다.
					  logseq.order-list-type:: number
					- [합성 스레드]([[브라우저/합성 스레드]]) 는 화면 출력을 담당한다. 사용자에게 출력할 최종 화면을 조립하는 역할을 수행한다.
					  logseq.order-list-type:: number
				- 메인 스레드가 복잡한 차트 연산을 처리 중이라도 합성 스레드는 분담된 업무인 스크롤 이벤트를 먼저 처리해 화면을 구성한다.
				  logseq.order-list-type:: number
				- 이때 처리 시간 차이로 인해 합성 스레드가 처리해 이동한 화면의 특정 지점과 메인 스레드가 처리한 해당 지점의 콘텐츠 상태 사이에 불일치가 발생할 수 있다.
				  logseq.order-list-type:: number
				- 사용자는 이를 렉(lag), 즉연으로 인식한다.
				  logseq.order-list-type:: number
		- Lenis
			- lenis는 사용자의 스크롤 입력을 가로채서 브라우저가 화면을 그리기 전에 자신이 계산한 부드러운 수치로 화면 이동을 강제한다.
				- 이를 위해 브라우저가 그리는 화면 이동을 우선 막아햐 한다.
				- `requestAnimationFrame(callback)`을 바탕으로 브라우저가 다음  화면을 그리기 전에 사용자가 lenis에서 지정한 위치로 이동하도록 강제한다.
				- 이 과정을 반복해 lenis 객체를 이용해 지정한 가속도에 따라 화면을 스크롤할 수 있다.
				- 기본 구조는 다음 샘플 코드에서 파악하라.
					- [fastlab/src/sample-codes/lenis/basic-structure-01.html at ff3d76e65980f393358b6f36128ae5c36b82de0b · vizualizr/fastlab · GitHub](https://github.com/vizualizr/fastlab/blob/ff3d76e65980f393358b6f36128ae5c36b82de0b/src/sample-codes/lenis/basic-structure-01.html)
					-
		- GSAP
			- 시간 단위로 애니메이션을 관리하는 라이브러리다.
			- lenis와 결합하려면 애니메이션 기준을 위치 기반으로 바꿔야 한다.
			-
- ## Troubleshooting
	-
- ## log
	- [[2026-01-30]] Page created.
- ### References
	- [Window: requestAnimationFrame() 메서드 - Web API | MDN](https://developer.mozilla.org/ko/docs/Web/API/Window/requestAnimationFrame)