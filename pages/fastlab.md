date-installed:: [[2025-01-01]]
date-updated:: [[2026-07-16]]
item-type:: #software
alias::
tags::
ai-sourced:: 
lifecycle::
outcome::
host::

- ## Introduction
	- node.js project folder to run a various test for o-m.kr
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
	-
- ## Steps
	-
- ## Troubleshooting
	-
- ## log
	- [[2026-07-16]] Page created.
		- `vitest` 추가
	- [[2026-07-17]] css 처리 속도 개선을 위해 불필요한 css 처리 파이프라인을 정리.
		- 09:30 postCSS 제거. Vite가 tailwinds CSS를 처리하도록 강제함.
			- css pipeline rearranged
			- postCSS removed.
			- vite is sole in charge of css handling with tailwindcss plugin
		- DONE 09:52 tailwind CSS 인텔리센스 작동 불가 문제 해결 중
		  :LOGBOOK:
		  CLOCK: [2026-07-17 Fri 09:53:20]--[2026-07-17 Fri 10:08:31] =>  00:15:11
		  :END:
			- 우선 불필요한 확장 기능을 모두 껐음.
			- 아래에서 "strings": "on"` 뒤에 쉼표 안 찍어서 에러 난 거임. 해결 완료.
			- ```json
			      "editor.quickSuggestions": {
			          "strings": "on",
			          "other": "offWhenInlineCompletions",
			          "comments": "off",
			      }
			  ```
			- 현재 tailwind css 인텔리센스 정상 작동함.
- ### References
	-