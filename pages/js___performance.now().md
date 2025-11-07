date-created:: [[2025-10-23]]
date-modified::
division:: [[makr]]
stack:: frontend
tags:: Web API, performance, timing, Date.now, 개념정리
type::
status:: [[ai-generated]]

- ## Summary
	- `performance.now()`는 고해상도 시간 측정(High Resolution Time)을 위한 Web API 메서드이다.
	- 문서 로드 시작 시점(`time origin`)과 같은 고정된 기준점으로부터 경과된 시간을 마이크로초 정밀도의 밀리초 단위(`DOMHighResTimeStamp`)로 반환한다.
	- 핵심 특징은 **단조롭게 증가(monotonically increasing)**한다는 점이다. 즉, 시스템 시계 변경에 영향을 받지 않아 항상 이전 호출 값보다 크거나 같으며, 정확한 시간 간격 측정에 필수적이다.
	- 이는 시스템 시계에 의존하여 값이 역행할 수 있는 `Date.now()`와의 주요 차이점이다.
- ## Steps
	- ### **1. `performance.now()` 동작 방식**
		- **입력물:** 없음.
		- **동작 (처리):**
			- 호스트 환경(브라우저 등) 내부의 고해상도 타이머 값을 읽는다.
			- 이 타이머는 시스템 시계와 독립적이며, 문서 로드 시작 시점(`time origin`)을 0으로 하여 계속 증가한다.
			- `time origin`으로부터 현재까지 경과된 시간을 `DOMHighResTimeStamp` 타입으로 계산하여 반환한다.
		- **출력물:** `DOMHighResTimeStamp` 값 (숫자, 밀리초 단위, 마이크로초 정밀도).
	- ### **2. 단조로운 증가 (Monotonic Increase)의 의미와 중요성**
		- **정의:** `performance.now()`는 동일 문서 내에서 호출될 때마다 항상 이전 호출 값보다 크거나 같은 값을 반환하는 것이 보장된다. 시간이 거꾸로 흐르지 않는다.
		- **이유:** 시스템 시계가 아닌, 영향을 받지 않는 내부 타이머를 사용하기 때문이다.
		- **중요성:** 코드 실행 시간, 애니메이션 프레임 간격 등 정확한 **시간 간격(duration)**을 측정할 때 필수적이다.
	- ### **3. `Date.now()`와의 비교**
		- **`Date.now()`:**
			- **기준:** 운영체제의 시스템 시계 (사용자 또는 시스템에 의해 변경 가능).
			- **동작:** Unix Epoch(1970-01-01 UTC)로부터 경과된 시간을 밀리초(정수)로 반환.
			- **문제점:** 시스템 시간 변경 시 값이 이전 호출보다 작아질 수 있어, 시간 간격 측정에 오류 발생 가능.
		- **`performance.now()`:**
			- **기준:** 문서 로드 시작 시점 (`time origin`, 고정).
			- **동작:** `time origin`으로부터 경과된 시간을 고해상도 밀리초(부동 소수점)로 반환.
			- **장점:** 단조롭게 증가하여 시간 간격 측정의 정확성 보장.
	- ### **4. 주요 용도**
		- 자바스크립트 코드 블록의 실행 시간 측정 (성능 벤치마킹).
		- `requestAnimationFrame` 등과 함께 사용하여 부드러운 애니메이션 구현.
		- 사용자 인터랙션 반응 시간 등 정밀한 시간 간격 측정.
- ## Troubleshooting
	- `performance.now()`가 반환하는 값은 특정 시각(wall clock time)을 나타내는 것이 아니라, 특정 기준점으로부터의 경과 시간(elapsed time)이다. 현재 시각이 필요하면 `Date.now()`를 사용해야 한다.
- ## log
	- [[2025-10-23]] Page created.
- ### References
	- [[performance.now() - Web APIs | MDN]]