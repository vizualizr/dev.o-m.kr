status:: [[ai-proofed]]
alias:: LLM 기반 프로그래밍 에이전트를 사용하는 방법
date-created:: [[2025-11-19]]
date-modified::  [[2025-11-21]]

- ## Summary
	- Make problems into a smallest piece as possible.
	  logseq.order-list-type:: number
		- AI is not able to handle the big picture. You have to do it.
		  logseq.order-list-type:: number
		- [[antigravity]] autonomously breaks down a chunk of task into small tasks.
		  logseq.order-list-type:: number
- ## Steps
	- ### folder structure
		- The folder includes `.agent` folder becomes your antigravity project folder.
		- ```bash
		  .agent
		  ├── daily-logs/             # 일별 작업 기록 (2026-01-20.md 등)
		  ├── plans/                  # 시스템 설계 및 계획 문서
		  ├── rules/                  # 핵심 가이드라인 (project-guideline.md, tech-stack.md 등)
		  ├── usr/                    # 사용자가 관리하는 커스텀 계획, 프로토타입, 템플릿
		  │   ├── plans/
		  │   ├── prototypes/
		  │   └── templates/
		  ├── workflows/              # 자동화된 작업 절차 정의 (backup_brain.md 등)
		  └── overview.md             # 프로젝트 헌장 및 최상위 개요
		  ```
- ## Troubleshooting
	-
- ## log
	- [[2025-11-19]] Page created.
- ### References
	- [[@Augmented Coding: Beyond the Vibes]]