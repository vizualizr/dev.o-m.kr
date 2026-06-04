date-installed:: [[2026-05-30]] 
date-updated:: [[2026-05-30]]
item-type:: #software
alias::
tags::
ai-sourced:: 
lifecycle:: pooled
outcome::
host::

- ## Introduction
	-
- ## Steps
	- ### wofkflow
		- 로컬(로그식 그래프 폴더)
			- d:\yonggeun\porter\git\o-m.kr\journal\
			- 트리거
				- 로컬에서 rsync 실행하면
				- 호스트(p1@windows 11)에서 리모트로 로그식 그래프 폴더 전송
		- ubuntu@oci
			- 우분투가 파일 변경 감지
			- quartz가 자동으로 정적 html 파일로 빌드
			- 빌드 완료하면 git이 자동으로 git commit한 뒤 깃허브로 push
			- 깃허브에서 GitHub Actions가 빌드 후 github page로 배포
- ## Troubleshooting
	- DOING [[2026-05-30]] Installation testing on Big Sur
	  :LOGBOOK:
	  CLOCK: [2026-05-30 Sat 12:19:54]
	  :END:
		- 설치
		  logseq.order-list-type:: number
			- logseq.order-list-type:: number
			  ```bash
			  
			  git clone https://github.com/jackyzha0/quartz.git
			  
			  # 2. 다운로드된 quartz 폴더로 이동
			  cd quartz
			  
			  # 3. 필요한 패키지(의존성) 설치 (시간이 조금 걸릴 수 있습니다)
			  npm i
			  
			  # 4. Quartz 초기화 스크립트 실행
			  npx quartz create
			  ```
- ## log
	- [[2026-05-30]] Page created.
- ### References
	-