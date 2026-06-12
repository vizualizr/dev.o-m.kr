date-created:: [[2025-07-22]]
date-updated:: [[2026-06-09]] 
alias::
tags:: 웹팩, webpack, 비트
ai-sourced:: #ai-proofed 
division::
stack::
type::
public:: true

- ## Summary
	- [[자바스크립트 엔진과 런타임]]의 개념을 우선 이해하라.
- ## Steps
	- ### vite의 역할과 기존 번들러와의 차이점
		- node.js는 비동기 처리로 [웹 서버의 성능을 대폭 개선]([[자바스크립트 엔진과 런타임]])했다.
		- node.js 기반의 개발이 활성화되면서 다양한 npm 모듈이 등장했다. 이 모듈을 프론트엔드 개발에도 사용하기 위해 웹팩(webpack)과 같은 번들러를 사용했다.
			- 웹팩에서는 다양한 npm 모듈로 구성된 프론트엔드 자바스크립트 파일의 의존성을 체계적으로 관리할 수 있었다. 이를 위해 CommonJS의 `require`와 `import`를 지원했다.
			- 이를 위해 index.html이라는 하나의 진입점에서 `main.js`라는 파일을 모듈 형태로 불러오면 다른 의존성 (자바스크립트 파일)을 구조적으로 관리할 수 있도록 했다.
			- 웹팩은 최초 번들링 전에 반드시 아래와 같은 의존성 그래프를 작성해야 했다. 이후에 HMR(Hot Module Replacement)로 변경된 모듈만 교체할 수 있었지만 속도가 느렸다. 변경 사항을 검토한 후에 의존성 그래프를 다시 작성해야 하기 때문이다.
			- ```text
			  main.js
			    ├── import './style.css'
			    ├── import * as d3 from 'd3'
			    └── import './chart.js'
			              └── import './utils.js'
			  ```
			- 때문에 프로젝트가 커질 수록 개발 중 번들링이 끝나기를 기다리는 시간이 길어졌다.
		- vite는 웹팩에서 거쳐야 하는 번들링 대기 시간을 줄이기 위해 등장했다. 가장 큰 차이점은 개발 모드에서 번들링 과정을 생략한 점이다.
			- vite는 ES2015에서 제시한 `import`를 중심으로 설계했다. 때문에 개발 모드(`npm run dev`) 에서 사용자가 직접 작성한 파일은 브라우저에 기본 탑재한 ES 모듈이 직접 처리한다. 단 npm 모듈은 vite가 esbuild로 사전 번들링해서 캐시에 저장해 둔다. 개발 모드에서 번들링 없이 브라우저가 직접  `import`를 처리하므로 더욱 빠른 속도를 달성할 수 있었다.
- ## Troubleshooting
	- 프로젝트 폴더의 절대 경로 변경 후 비트 서버에서 의존성 검사 실패 메시지가 뜰 경우 [[2026-06-09]]
		- 직접적인 원인은 절대 경로 변경이므로
		- 우선 설정 파일에 아래 추가한 다음,
		- ```js
		  export default defineConfig({
		    ...
		    optimizeDeps: {
		      // 비트 서버 시작 시점에 의존성(라이브러리) 검사를 할 파일을 직접 지정하는 옵션이다.
		      // 여기에 적히지 않은 html 파일도 브라우저가 요청하면
		      // 실시간으로 파일을 컴파일 하므로 HMR은 정상 작동한다.
		      entries: [
		        "index.html",
		        "**/end/index.html",
		        "**/start/index.html",
		        "**/started.index.html",
		      ],
		    },
		  });
		  ```
		- 아래 명령어를 실행한다.
			- ```bash
			  Remove-Item -Recurse -Force node_modules\.vite
			  npm run dev
			  ```
- ## log
	- [[2026-05-13]] Page created.
- ### References