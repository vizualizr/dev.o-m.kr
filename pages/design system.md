date-created:: [[2026-01-06]]
date-updated:: [[2026-08-08]] 
division::
stack::
tags::
type::
alias:: 디자인 시스템, 디자인시스템
public:: false

- ## Summary
	- Documenting the design system of [[o-m.kr]]
- ## Steps
	- ### considerations
		- #### Key concepts
			- dot:
			  id:: 6965e336-ea5d-4567-bfdc-b63d8afc24aa
				- Everything that exist alone together
			- line:
				- The place where dots and line plays on.
			- plane:
				- The place where dots and line plays on.
	- ### confirmations
		- From [Material design system](https://m3.material.io/) by Google
			- Implementation of [[design tokens]] [link](https://m3.material.io/foundations/design-tokens/overview#6a0933c0-50f5-4dd6-b055-b7c4ff2c1535)
		- #### visualization
			- #### guideline
				- > “STAAT /Random l-XI” ([Rendgen, 2020, p. 300](zotero://select/library/items/VPCLWFFR)) ([pdf](zotero://open-pdf/library/items/B956VGQY?page=304&annotation=7SFY3IBI))  복잡성 그대로를 있는 그대로 제시해야 하는가? 혹은 가시화를 위한 기본 논리가 개입해 복잡성을 줄여야 하는가?
				- #+BEGIN_IMPORTANT
				  Render complexity, then reveal the interaction.
				  #+END_IMPORTANT
					- Conflict is complex.
					- Present the complexity as it is seen in a glance.
						- Well visualized, the complexity must be beautiful and attractive as the pattern on the surface implies certain rules in
					- User's scrolling is an intention to dive into the presented complexity.
					- Thus complexity is an attractor.
					- Complexity is the result of iterated interaction between the relevant bodies.
				- If it is beautiful, it is an artwork.
	- ### Benchmarks
		- Look for information visualization projects by the Swiss design agencies.
			- [Superdot • Data Visualization](https://www.superdot.studio/projects/data-visualization)
	- ### test environment
		- layout test (compatible with #[[tailwind CSS]] )
			- https://www.tailwind-builder.site
		- #### considerations
			- [self-host penpot](https://penpot.app/self-host#options) via docker on ubuntu@OCI
				- tailwind export is available via community plugin
				- warnings
					- OCI Ubuntu에서 Docker로 설치 시 주요 참고사항
					  방화벽(Security List & UFW) 설정:
					  
					  Penpot 웹 인터페이스에 접근하기 위해 사용하는 포트(기본적으로 HTTP/HTTPS 또는 Docker 설정에 따른 포트)를 OCI 클라우드 콘솔의 VCN 보안 리스트(Security List)와 Ubuntu 내부 방화벽(ufw)에서 모두 열어주어야 합니다.
					  
					  리버스 프록시(Nginx / Caddy 등) 및 SSL:
					  
					  프로덕션 환경으로 운영할 경우, Docker 컨테이너 앞단에 Nginx나 Caddy 같은 리버스 프록시를 두고 Let's Encrypt를 통해 SSL(HTTPS)을 적용하는 것이 안전합니다.
			- [openpencil](https://github.com/open-pencil/open-pencil)
				- > 오픈펜슬은 캔버스 위에서 사각형을 예쁘게 배치하는 도구가 아니라, `Cursor`나 `Claude Code` 같은 AI 코딩 툴이 내 디자인을 읽고(MCP 서버 기능), 명령어로 "여기에 버튼 추가해 줘"라고 하면 AI가 알아서 UI를 그려주는 **AI-First 워크플로우**에 최적화한 도구임. #ai-generated
				  > Figma의 유료 개발자 모드(Dev Mode)를 완전히 대체하기 위해 만든 무료 오픈소스 프로그램
				- 프로젝트 자체가 극 초기 단계라 안 되는 게 많다.
- ## Troubleshooting
	-
- ## log
	- [[2026-01-06]] Page created.
- ### References
	- #### primary
		- /zotero
	-
	-