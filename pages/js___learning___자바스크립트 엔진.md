date-created:: [[2025-10-24]]
date-modified::
division:: [[makr]]
stack:: frontend
tags:: v8, performance, jit, devtools
type::
status:: [[ai-generated]]

- ## Summary
	- 프론트엔드 개발자는 자바스크립트 엔진의 구성 요소와 작동 순서를 이해하면 성능 최적화, 디버깅, 프레임워크 내부 동작 해석, 메모리 관리에서 유리하다.
	- 본 문서는 주로 V8 기준을 중심으로 설명하되 엔진-중립 개념을 병기한다.
- ## Steps
	- Level 1: 엔진 기본 구성 요소 파악
		- 파서, 인터프리터, JIT 컴파일러, 가비지 콜렉션의 역할과 전체 실행 순서를 이해한다.
	- Level 2: 실행 흐름과 메모리 구조 이해
		- 인터프리터가 초기 비최적화 실행을 담당하는 방식과 JIT가 최적화된 네이티브 코드를 생성해 참조를 교체하는 과정을 이해한다.
	- Level 3: 최적화 판단 기준과 피드백 구조 분석
		- 핫스팟 감지, 타입 안정성, 인라인 캐시, 런타임 피드백이 최적화 결정에 미치는 영향을 학습한다.
	- Level 4: 가비지 콜렉션 세부 전략과 클로저 상호작용
		- 마크 앤 스윕, 세대별 수집, 약한 참조(WeakMap/WeakSet)와 클로저가 메모리 보유에 미치는 영향을 이해한다.
	- Level 5: DevTools 지표와 엔진 단계 연결
		- Performance 탭의 Scripting, Layout, Recalculate Style 항목을 엔진의 실행 단계와 대응시켜 해석하는 법을 익힌다.
	- Level 6: Astro 기반 데이터 저널리즘과 엔진 상호작용
		- 컴파일 타임 렌더링, island hydration, 클라이언트 번들 최소화가 엔진 최적화 경로에 미치는 영향을 분석한다.
	- Level 7: 엔진별 차이점과 프레임워크 대응 전략
		- V8, SpiderMonkey, JavaScriptCore 핵심 차이를 파악하고 프레임워크 설계·배포 전략에 반영한다.
	- ### Elements Hierachy
		- **소스 레이어**
			- **Source code** — 개발자가 작성한 고수준 코드.
			- collapsed:: true
			  
			  **파서 (Parser)** — 토큰화와 문법 분석을 수행해 AST를 생성해요.
				- **스캐너/렉서 (Scanner/Lexer)** — 입력을 토큰으로 분해해요.
		- **구문·중간 표현 레이어**
			- **추상 구문 트리 (AST)** — 파서가 생성한 문법적 구조(데이터 구조).
			- **저수준 중간 표현 / 바이트코드 전 단계 IR** — (요청시 더 상세히 표기 가능)
		- **인터프리터 / 바이트코드 레이어**
			- **인터프리터 (예: Ignition)** — 바이트코드를 해석·실행하고, **프로파일링을 위한 실행 데이터를 생성**해요.
				- **바이트코드 생성기 (Bytecode Generator)** — AST/IR로부터 바이트코드를 생성해요.
				- **바이트코드 핸들러/디스패처 (Bytecode Handler/Dispatcher)** — 각 바이트코드 명령을 처리해요.
			- **바이트코드 (Bytecode)** — VM이 해석하거나 JIT의 입력으로 사용하는 중간 코드 형식.
		- **프로파일링·피드백 레이어**
			- **프로파일러 (Profiler)** — 인터프리터 실행 중 생성된 데이터를 **수집·분석**하여 JIT 최적화 판단에 사용해요.
		- **JIT / 최적화 레이어**
			- **최적화 컴파일러 (예: TurboFan)** — 프로파일과 IR을 이용해 고성능 머신코드를 생성해요.
			- **JIT-generated native code / 최적화된 기계어 코드** — 런타임에 생성된 실행 가능한 머신코드(네이티브 코드).
		- **런타임 시스템 레이어**
			- **런타임 시스템 (Runtime System)** — 실행 인프라 전반을 담당해요.
				- **메모리 관리자 (Memory Manager)** — 힙·스택·메모리 할당 정책을 관리해요.
					- collapsed:: true
					  
					  **메모리 힙 (Memory Heap)** — 객체 할당 영역.
						- 신규 공간 (New Space / Young Generation)
						- 기존 공간 (Old Space / Old Generation)
						- 코드 공간 (Code Space) — JIT/컴파일러가 생성한 코드 저장소.
						- 대형 객체 공간 (Large Object Space)
					- collapsed:: true
					  
					  **콜 스택 (Call Stack)** — 실행 프레임과 지역 변수 보관 영역.
						- **실행 컨텍스트 (Execution Context)** — 함수 호출 시 생성되는 렉시컬 환경·스코프·변수 상태를 보관하는 데이터 구조(콜 스택에서 관리됨).
					- collapsed:: true
					  
					  **가비지 컬렉터 (GC, 예: Orinoco)** — 메모리 회수를 담당해요.
						- 마이너 GC (Minor GC / Scavenger)
						- 메이저 GC (Major GC / Mark-Sweep / Mark-Compact)
				- **실행 제어 (Execution Control)** — 최적화·비최적화 전환과 실행 흐름 제어.
					- **비최적화(Deoptimizer) 핸들러** — 최적화 가정 위배 시 복원 처리.
				- **객체 표현 시스템 (Object Representation System)** — 런타임 객체 모델을 정의해요.
					- 히든 클래스 / 셰이프 (Hidden Classes / Shapes)
					- 인라인 캐시 (Inline Caches, ICs)
				- **예외 처리 메커니즘 (Exception Handling Mechanism)**
				- **호스트 바인딩/인터페이스 (Bindings/Interface to Host Environment)** — 외부 API·I/O와의 연결.
				- **내부 유틸리티 및 빌트인 객체/함수 (Internal Utilities & Built-ins)**
		- **Wasm 서브시스템 (V8 통합 관점)**
			- **WebAssembly 엔진** — Wasm 모듈 디코드·컴파일·실행 담당.
				- **Wasm 디코더 (Wasm Decoder)**
				- **Liftoff** (Wasm 베이스라인 컴파일러)
				- **TurboFan** (Wasm 최적화 컴파일러) — JS 최적화 파이프라인과 역할이 유사해요.
	- ### 저수준에서 고수준으로 정렬된 실행 단위
		- Source code
			- 사람이 작성하는 고수준 언어 코드(예: JavaScript, TypeScript)예요. 가장 추상화된 표현이며 최종적으로 위 단계들로 변환되어 실행돼요.
			- ```js
			  // 반복적인 계산을 수행하는 함수 (최적화 대상)
			  function calculateSum(n) {
			  // 삼각수 연산 (0 + 1 + 2 + ... + (n-1))을 시작한다.
			    let sum = 0;
			    // 충분히 많은 반복을 통해 '뜨겁게' 만듭니다.
			    for (let i = 0; i < n; i++) {
			      sum += i; // 단순한 덧셈 연산
			    }
			    return sum;
			  }
			  
			  // 위 함수를 여러 번 호출하여 JIT 컴파일을 유도하는 함수
			  function runCalculations() {
			    console.log("계산 시작...");
			    const startTime = performance.now();
			  
			    // calculateSum 함수를 매우 많이 호출합니다 (예: 10만 번)
			    // 이 반복 호출이 calculateSum을 '뜨겁게' 만듭니다.
			    for (let j = 0; j < 100000; j++) {
			      calculateSum(1000); // 함수 내부 반복 횟수
			    }
			  
			    const endTime = performance.now();
			    console.log(`계산 완료! 총 소요 시간: ${(endTime - startTime).toFixed(2)}ms`);
			  }
			  
			  // 함수 실행
			  runCalculations();
			  
			  // 추가 호출 (이미 최적화된 상태에서 실행될 가능성이 높음)
			  console.log("추가 계산 시작 (최적화 후)...");
			  const startTimeOptimized = performance.now();
			  calculateSum(100000); // 단일 호출
			  const endTimeOptimized = performance.now();
			  console.log(`추가 계산 완료! 소요 시간: ${(endTimeOptimized - startTimeOptimized).toFixed(2)}ms`);
			  ```
		- 추상구문트리(Abstract Syntax Tree)
			- 파서가 생성하는 구조화된 문법 트리예요. 코드의 문법적 구조와 의미를 담고 있어 컴파일러/트랜스파일러가 분석·변환할 때 사용해요.
			- 아래 코드는 위 코드를 변환한 AST를 JSON으로 번역한 내용을 간추렸다. 해당 코드의 AST 전체는 다음 링크를 참조하라.
				- [AST explorer](https://astexplorer.net/#/gist/6b96153e5c5f47ed71b8b8eccd05efb8/latest)
			- ```json
			  {
			    "type": "Program",
			    "body": [
			      // 1. calculateSum 함수 선언 부분
			      {
			        "type": "FunctionDeclaration",
			        "id": { "type": "Identifier", "name": "calculateSum" },
			        "params": [ { "type": "Identifier", "name": "n" } ],
			        "body": {
			          "type": "BlockStatement",
			          "body": [
			            // let sum = 0;
			            {
			              "type": "VariableDeclaration",
			              "kind": "let",
			              "declarations": [
			                {
			                  "type": "VariableDeclarator",
			                  "id": { "type": "Identifier", "name": "sum" },
			                  "init": { "type": "Literal", "value": 0 }
			                }
			              ]
			            },
			            // for (let i = 0; i < n; i++) { ... }
			            {
			              "type": "ForStatement",
			              "init": { // let i = 0;
			                "type": "VariableDeclaration", "kind": "let",
			                "declarations": [{ "type": "VariableDeclarator", "id": { "type": "Identifier", "name": "i" }, "init": { "type": "Literal", "value": 0 } }]
			              },
			              "test": { // i < n;
			                "type": "BinaryExpression", "operator": "<",
			                "left": { "type": "Identifier", "name": "i" },
			                "right": { "type": "Identifier", "name": "n" }
			              },
			              "update": { // i++;
			                "type": "UpdateExpression", "operator": "++", "argument": { "type": "Identifier", "name": "i" }
			              },
			              "body": {
			                "type": "BlockStatement",
			                "body": [
			                  // sum += i;
			                  {
			                    "type": "ExpressionStatement",
			                    "expression": {
			                      "type": "AssignmentExpression", "operator": "+=",
			                      "left": { "type": "Identifier", "name": "sum" },
			                      "right": { "type": "Identifier", "name": "i" }
			                    }
			                  }
			                ]
			              }
			            },
			            // return sum;
			            {
			              "type": "ReturnStatement",
			              "argument": { "type": "Identifier", "name": "sum" }
			            }
			          ]
			        }
			      },
			  
			      // 2. runCalculations 함수 선언 부분 (일부 생략)
			      {
			        "type": "FunctionDeclaration",
			        "id": { "type": "Identifier", "name": "runCalculations" },
			        "params": [],
			        "body": {
			          "type": "BlockStatement",
			          "body": [
			            // console.log("계산 시작...");
			            { /* CallExpression for console.log */ },
			            // const startTime = performance.now();
			            { /* VariableDeclaration calling performance.now */ },
			            // for (let j = 0; j < 100000; j++) { ... }
			            {
			              "type": "ForStatement",
			              // ... (init, test, update for j) ...
			              "body": {
			                "type": "BlockStatement",
			                "body": [
			                  // calculateSum(1000);
			                  {
			                    "type": "ExpressionStatement",
			                    "expression": {
			                      "type": "CallExpression",
			                      "callee": { "type": "Identifier", "name": "calculateSum" },
			                      "arguments": [ { "type": "Literal", "value": 1000 } ]
			                    }
			                  }
			                ]
			              }
			            },
			            // const endTime = performance.now();
			            { /* VariableDeclaration calling performance.now */ },
			            // console.log(`...`);
			            { /* CallExpression for console.log with TemplateLiteral */ }
			          ]
			        }
			      },
			  
			      // 3. runCalculations(); 함수 호출
			      {
			        "type": "ExpressionStatement",
			        "expression": {
			          "type": "CallExpression",
			          "callee": { "type": "Identifier", "name": "runCalculations" },
			          "arguments": []
			        }
			      },
			  
			      // 4. console.log("추가 계산 시작...");
			      { /* CallExpression for console.log */ },
			  
			      // 5. const startTimeOptimized = performance.now();
			      { /* VariableDeclaration calling performance.now */ },
			  
			      // 6. calculateSum(100000); 함수 호출
			      {
			        "type": "ExpressionStatement",
			        "expression": {
			          "type": "CallExpression",
			          "callee": { "type": "Identifier", "name": "calculateSum" },
			          "arguments": [ { "type": "Literal", "value": 100000 } ]
			        }
			      },
			  
			      // 7. const endTimeOptimized = performance.now();
			      { /* VariableDeclaration calling performance.now */ },
			  
			      // 8. console.log(`...`);
			      { /* CallExpression for console.log with TemplateLiteral */ }
			    ]
			  }
			  ```
			-
		- Internal Intermediate Representation (중간 표현)
		  collapsed:: true
			- **입력물 (Input):**
				- 추상 구문 트리 (AST) 또는 이전 단계의 다른 IR.
			- **동작 (Processing): 컴파일러의 내부 작업**
				- **변환:** 컴파일러는 소스 코드의 복잡한 구조(AST)를 분석하여, 최적화를 수행하거나 특정 타겟(바이트코드, 기계어)으로 코드를 변환하기 더 쉬운 형태로 코드를 재구성합니다. 이 재구성된 형태가 IR입니다.
				- **분석 및 최적화:** IR은 종종 코드의 제어 흐름(Control Flow Graph), 데이터 흐름(Data Flow Analysis) 등을 분석하고, 불필요한 연산 제거, 코드 이동 등 다양한 최적화 패스(Optimization Pass)를 적용하기 용이하도록 설계됩니다.
			- **출력물 (Output):**
				- 더 최적화되었거나 다음 변환 단계에 적합한 형태의 IR, 또는 최종적인 바이트코드/기계어 코드.
		- collapsed:: true
		  
		  Bytecode 또는 VM instruction
			- 가상머신용 중간 코드예요. 플랫폼 독립적이며 인터프리터 또는 바이트코드 기반 JIT가 실행·변환에 사용해요.
		- collapsed:: true
		  
		  Low-level intermediate representation IR
			- 컴파일러 내부에서 사용하는 중간 표현으로 레지스터, 제어 흐름, 타입 정보에 가깝게 기술돼요. 최적화 패스가 적용되는 수준이에요.
		- collapsed:: true
		  Machine instruction
			- CPU가 직접 수행하는 단일 명령어의 이진 인코딩이에요.
		- Assembly
		  collapsed:: true
			- machine instruction을 사람이 읽기 쉬운 텍스트로 표기한 표현이에요. 기계어와 1:1 대응해요.
		- collapsed:: true
		  
		  JIT-generated native code
			- 런타임 JIT가 프로파일을 바탕으로 생성한 최적화된 머신 코드예요. 네이티브 코드 범주에 속하지만 생성 시점과 특성이 명확해요.
		- collapsed:: true
		  
		  Machine code 또는 Native code
			- 여러 instruction이 연속된 이진 코드예요. AOT로 생성된 바이너리와 메모리 상에서 실행 가능한 JIT-생성 코드 모두를 포함해요.
- ## Troubleshooting
	- 성능 병목 분석: Performance 탭의 Scripting/Layout/Recalculate Style 병목은 엔진의 실행 단계별 병목 구간을 기준으로 원인을 추적한다.
	- 메모리 누수 감지: 이벤트 핸들러·클로저 등 참조가 해제되지 않는 경우 가비지 콜렉션의 도달성 규칙을 기준으로 누수 지점을 찾는다.
	- 최적화 실패 진단: 메모이제이션·인라이닝이 기대 성능을 내지 못하면 런타임 타입 안정성 및 인라인 캐시 상태를 점검한다.
	- 렌더링 지연 해결: DOM 조작으로 인한 지연은 스타일 계산 → 레이아웃 → 페인트 순서에 따라 병목을 분리하여 우선순위를 조정한다.
	- Astro island hydration 병목: island 활성화 지연은 hydration 시점의 JS 실행 경로와 JIT 최적화 준비 상태를 기준으로 분석한다.
- ## log
	- [[2025-10-24]] Page created.
- ### References
	- V8 공식 문서: https://v8.dev/
	- Chrome DevTools Performance Guide: https://developer.chrome.com/docs/devtools/performance/
	- Astro 공식 문서: https://docs.astro.build/