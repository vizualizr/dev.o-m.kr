date-created:: [[2025-08-01]] 
date-modified:: [[2026-01-24]]
division::
stack::
tags:: LLM, AI
type::
alias::
public:: true

- ## Summary
	-
- ## Steps
	- ### Model Comparison as of [[2026-01-24]] as a coding agent on [[antigravity]]
		- | Model                          | Fitness| Features                                                                 | Strengths as a Coding Agent                                                                                 | Usage Scenarios                                |
		  |--|--|--|--|--|
		  | Gemini 3 Pro High | ★★★★★ |Architect. [:br]Optimized for designing complex system architectures and reviewing logical integrity across multiple files |Excels at identifying dependencies across the entire codebase and logically explaining 'why this approach is better.' Strong in proactive suggestions (A') |Initial project schema design, complex business logic implementation, performance optimization strategies |
		  | Gemini 3 Pro Low | ★★★★☆ (Excellent) |Hackathon player. Performance is close to High while latency is significantly lower|Ideal for fast TDD workflow cycles (write failing test → implement code → refactor). Maintains high code quality without breaking developer rhythm |Routine function implementation, unit test creation, UI component development |
		  | Gemini 3 Flash | ★★☆☆☆ (Support) |Code vending machine. Very lightweight and fast, strong in pattern matching rather than complex reasoning.|More suitable for real-time code completion (autocomplete) and syntax error checking than for large-scale refactoring or new feature development |Documentation, simple comment generation, real-time typo correction |
		- | 모델명                        | 적합도        | 특징                                                                 | 코딩 에이전트 강점                                                                                          | 사용 시점                                      |
		  |--|--|--|--|--|
		  |Gemini 3 Pro Hgith| ★★★★★|설계자.[:br]복잡한 시스템 아키텍처 설계와 다중 파일 간 논리적 무결성 검토에 최적화 |전체 코드베이스 의존성을 파악하며 '왜 이 방식이 더 나은가'를 논리적으로 설명. 선제적 제안(A')에 강점             |프로젝트 초기 스키마 설계, 복잡한 비즈니스 로직 구현, 성능 최적화 전략 수립 |
		  |Gemini 3 Pro Low | ★★★★☆ (우수) |해커톤 플레이어. 성능은 High에 근접하면서도 응답 지연 시간(Latency)이 낮음              |TDD 워크플로우(실패하는 테스트 작성 → 코드 구현 → 리팩토링)의 빠른 사이클에 최적. 높은 코드 품질과 빠른 속도 유지 |일상적인 함수 구현, 단위 테스트 작성, UI 컴포넌트 개발 |
		  |Gemini 3 Flash| ★★☆☆☆ (보조) |코드 자판기. 매우 가볍고 빠르며, 복잡한 추론보다는 패턴 매칭에 강함                 |대규모 리팩토링이나 새로운 기능보다는 실시간 코드 완성(autocomplete)과 문법 오류 확인에 적합                        |문서화, 간단한 주석 생성, 실시간 오타 교정     |
- ## Troubleshooting
	-
- ## log
	- [[2026-01-24]] Page created.
- ### References
	-
- [[Gemini CLI]] is assissting this project on [[vs code]]