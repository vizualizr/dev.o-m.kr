date-created:: [[2026-02-12]]
date-updated::
division::
stack::
tags:: GSAP, css transform
type::
public:: true
ai-sourced:: #ai-proofed

- ## Summary
	- SVG 요소의 크기와 좌표를 변경하는 방법에는 두 가지가 있다.
		- SVG 요소의 크기 및 좌표 속성을 직접 변경
		  logseq.order-list-type:: number
		- 합성 레이어 위에서 CSS transform으로 해당 요소의 위치와 크기를 변경.
		  logseq.order-list-type:: number
	- 두 가지 방식의 차이는 **"누가 계산하느냐(CPU vs GPU)"**와 **"언제 계산하느냐(렌더링 파이프라인)"**에 있다.
- ## Steps
	- ### 비교표
		- | **비교 항목** | **SVG 속성 변경 (x, y, cx, cy)** | **CSS Transform (translate(x, y))** |
		  | **방식** | **물리적인 기하학적 구조** 자체를 변경 | 기하학적 구조는 두고 **시각적인 레이어**만 이동 |
		  | **작동 원리** | 지정된 실제 좌표로 브라우저가 다시 그림 | 해당 요소의 기하학적인 속성(DOM)은 그대로 유지한 채, <br />요소를 **독립된 비트맵 레이어로 분리한 뒤 GPU에서 Transform 연산을 적용하여 화면에 합성(Composite)한다.**|
		  | **렌더링 과정** | 레이아웃 재계산(Reflow) 및 픽셀 리페인트(Repaint) | 레이아웃 계산을 건너뛰고 합성(Composite)만 수행 |
		  | **연산 주체** | **CPU** | **GPU (하드웨어 가속)** |
		  | **성능 (애니메이션)** | 매번 DOM을 재계산하므로 수천 개 요소를 변경하면 버벅임(프레임 드랍) 발생 | 스크롤 애니메이션(GSAP) 및 화면 전환에 절대적으로 유리|
		  | **기준점 (Origin)** | 항상 부모 SVG 전체 캔버스의 **좌측 상단(0,0)** 기준 | `transform-origin` 속성 사용 가능 (예: 정중앙 `50% 50%` 축 설정 용이) |
		  | **크기/위치 접근 방법** | `getBBox()`, `getBoundingClientRect()` 둘 다 **변경된 값** 반환 | `getBBox()`는 **적용 전 원본** 반환 <br />`getBoundingClientRect()`는 **적용 후 실제 화면 값** 반환 |
		  | **퍼센트(%)의 의미** | **부모 SVG 캔버스 너비**의 비율 | **요소 자기 자신 너비**의 비율 |
		  | **코드 예시** | `<rect x="100" y="50" width="10" height="10" />` | `<rect class="my-rect" ... />` + CSS `transform: translate(100px, 50px);` |
	- ### 브라우저의 CSS Transform 처리 방식
		- 메인 스레드에서 CSS Transform을 적용할 대상을 비트맵 이미지로 그려 참조 ID와 함께 GPU에 전송한다.
		- 메인 스레드는 다음 작업을 처리한다.
		- 이 때부터 해당 요소의 CSS transform 변경 사항은 합성 스레드가 담당한다.
		- 합성 스레드는 참조ID에 해당하는 요소를 독립된 레이어 위에 놓고 좌표, 크기 등의 변경 사항을 GPU에 지시한다.
		- GPU는 변경 사항을 적용해 최종 화면에 합성한다.
- ## Troubleshooting
	- ### 상황 별 적용 가이드
		- #### 초기 렌더링
		  logseq.order-list-type:: number
			- ##### SVG 속성 변경 (x, y, cx, cy)
			  logseq.order-list-type:: number
				- 요소의 속성값으로 위치와 크기를 결정
				  logseq.order-list-type:: number
				- 데이터를 기반으로 처음 차트를 "그릴 때"는 SVG 속성(`x`, `y`, `width`, `height`)을 사용해 정확한 좌표에 배치한다.
				  logseq.order-list-type:: number
				- 즉, 데이터의 값을 물리적인 픽셀 좌표로 변환(Scale)하여 초기 스냅샷을 완성한다.
				  logseq.order-list-type:: number
		- #### 스크롤 연계 애니메이션
		  logseq.order-list-type:: number
			- ##### CSS Transform
			  logseq.order-list-type:: number
				- 스크롤을 내릴 때 차트 전체가 옆으로 이동하거나, 요소가 부드럽게 나타나거나, 스크롤에 맞춰 크기가 커질 때는 무조건 **CSS Transform (GSAP의 `x`, `y` 속성)**을 사용한다.
				- *참고: GSAP에서 `gsap.to(element, {x: 100, y: 100})`라고 쓰면, 자동으로 CSS `transform: translate(100px, 100px)`을 적용한다.
		- #### 차트 업데이트
		  logseq.order-list-type:: number
			- 데이터 변경에 따라 차트가 변화하는 애니메이션은 목적에 따라 위 두 가지 방법을 혼용한다.
			  logseq.order-list-type:: number
				- ##### SVG 속성 변경 (x, y, cx, cy)
				  logseq.order-list-type:: number
					- logseq.order-list-type:: number
					  ```js
					  d3.select('rect').transition().duration(1000)
					    .attr('height', 100)
					    .attr('y', 50);
					  ```
					- GSAP의 `AttrPlugin` (예: `gsap.to(el, { attr: { ... } })`)을 사용해도 렌더링 결과(CPU 재계산)는 D3와 100% 동일하다
					  logseq.order-list-type:: number
					- **특징:** 가장 직관적이고 표준적인 D3 방식이다.
					  logseq.order-list-type:: number
					- **단점:** 매 프레임마다 CPU가 레이아웃을 다시 계산(Reflow)하므로, 움직이는 요소가 수백~수천 개라면 지연 발생 가능.
					  logseq.order-list-type:: number
				- ##### CSS Transform
				  logseq.order-list-type:: number
					- logseq.order-list-type:: number
					  ```js
					  // CSS에 transform-origin: bottom; 이 설정되어 있어야 함
					  d3.select('rect').transition().duration(1000)
					    .style('transform', 'scaleY(2)'); // 높이를 2배로
					  ```
					- **장점:** 아무리 막대가 많아도 **부드러운 움직임**을 보장한다.
					  logseq.order-list-type:: number
					- **주의점:** 테두리(`stroke`)가 있다면 테두리의 위아래 두께도 같이 늘어나는 왜곡 현상이 발생할 수 있다.
					  logseq.order-list-type:: number
		- #### 기타 화면 효과를 위한 복잡한 애니메이션
		  logseq.order-list-type:: number
			- `<canvas>`를 사용할 수 있으나 DOM 요소 수준의 상호작용성을 포기해야 한다. 
			  logseq.order-list-type:: number
			- [<canvas>: The Graphics Canvas element](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/canvas)를 참조하라.
			  logseq.order-list-type:: number
- ## log
	- [[2026-02-12]] Page created.
- ### References
	- [<canvas>: The Graphics Canvas element](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/canvas)
	- [translate() - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/transform-function/translate)
	- [transform - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/transform)
	-