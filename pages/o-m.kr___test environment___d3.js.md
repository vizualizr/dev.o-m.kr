date-created:: [[2026-08-13]]
date-updated:: [[2026-08-13]]
alias::
tags:: #obsidianized 
ai-sourced:: 
division::
stack::
type::
public:: true

- ## Summary
	- A testing environment for studying d3.js with [[D3.js in Action, Third Edition]].
	- The project is only to test the code in the book, [[D3.js in Action, Third Edition]]
- ## Steps
	- Folder location and settings
		- ```bash
		  PS D:\yonggeun\now\makr\projects\o-m.kr\fastlab> npm list
		  fastlab@0.0.0 D:\yonggeun\now\makr\projects\o-m.kr\fastlab
		  ├── @observablehq/plot@0.6.17
		  ├── @tailwindcss/vite@4.3.3
		  ├── autoprefixer@10.4.21
		  ├── d3@7.9.0
		  ├── daisyui@5.6.16
		  ├── flyonui@2.3.1
		  ├── lucide@1.24.0
		  ├── postcss@8.5.19
		  ├── tailwindcss@4.3.3
		  ├── vite-plugin-devtools-json@0.3.0
		  ├── vite-plugin-list-directory-contents@1.4.5
		  ├── vite@7.0.5
		  └── vitest@4.1.10
		  ```
	- How to start
		- ```bash
		  npm run dev
		  ```
	- Current github repo
		- ```bash
		  PS D:\yonggeun\now\makr\projects\o-m.kr\fastlab> git remote -v
		  origin  git@github.com:vizualizr/fastlab.git (fetch)
		  origin  git@github.com:vizualizr/fastlab.git (push)
		  ```
- ## Troubleshooting
	-
- ## log
	- [[2026-08-13]] Page created.
		- 예제 코드 학습 외에 불필요한 코드는 모두 삭제했음.
		- `d3-in-action`폴더는 의존성 검사를 하지 않도록 아래처럼 설정을 수정.
			- ```js
			    optimizeDeps: {
			        entries: ["index.html", "src/main.js"], // 엔트리 파일을 명시적으로 지정, 이렇게 하면 d3-in-acton 폴더 아래 있는 파일의 의존성 검사를 건너뛴다.
			    },
			  ```
			- 즉 위에서 지정한 파일만 의존성 검사를 수행한다.
- ### References
	-