date-created:: [[2026-07-29]]
date-updated:: [[2026-07-29]]
alias:: o-m.kr/design system
tags::
ai-sourced:: 
division::
stack::
type::
public:: true

- ## Summary
	- design system test environment
- ## Steps
	- ### stacks
		- [[d3.js]], [[GSAP]], [[lenis]]
		- [[DaisyUI]] on [[tailwindcss]], [[lucide icons]]
	- ### environment setup
		- 아래 순서로 구성
		  logseq.order-list-type:: number
			- logseq.order-list-type:: number
			  ```bash
			  # 1. 폴더 초기화
			  npm init -y
			  
			  # 2. 개발용 빌드 및 스타일 관련 패키지
			  npm install -D vite tailwindcss @tailwindcss/vite daisyui@latest
			  
			  # 3. 런타임 라이브러리 (D3, GSAP, Lenis 스크롤, Lucide 아이콘)
			  npm install d3 gsap lenis lucide
			  ```
			- `vite.config.js` 설정
			  logseq.order-list-type:: number
				- logseq.order-list-type:: number
				  ```js
				  import { defineConfig } from 'vite';
				  import tailwindcss from '@tailwindcss/vite';
				  
				  export default defineConfig({
				    plugins: [
				      tailwindcss(),
				    ],
				  });
				  ```
			- 필요한 `css`, `js`, `html` 파일 추가
			  logseq.order-list-type:: number
			- vite 서버 실행
			  logseq.order-list-type:: number
				- logseq.order-list-type:: number
				  ```bash
				  # 서버 실행
				  npx vite
				  ```
- ## Troubleshooting
	-
- ## log
	- [[2026-07-28]] 설정 완료. 속도 만족함. 매우 빠름 localhost에서 실행
	- [[2026-07-29]] Page created.
	- [[2026-08-13]] 아래 사항 정상 작동 확인
		- html에서 d3.js 호출해 사용
- ### References
	-