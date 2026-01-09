item-type:: [[software]]
outcome:: gemini-cli 및 Antigravity 환경 변수 설정 및 쿼터 문제 해결 방안 정리
date-of-installation:: 
date-of-update:: [[2026-01-03]]
alias:: gemini-cli-auth-guide
status:: [[ai-generated]]

- ## Introduction
	- gemini-cli 사용을 위한 윈도우 환경 변수 설정 및 인증 방식 파악.
	- Legacy 버전의 Google Workspace에 속하는 계정을 사용할 때 발생하는 Gemini-cli 인증 오류 해결 방안 모색.
- ## Steps
	- ### 환경 변수 설정
		- gemini-cli가 참조하는 API 키 환경 변수명은 `GEMINI_API_KEY`임.
		- 윈도우 시스템 환경 변수 또는 PowerShell(`$env:GEMINI_API_KEY`)을 통해 설정 가능.
	- **### 인증 및 계정 전환**
		- 계정이나 API 키를 변경해도 로컬의 `GEMINI.md` 및 대화 이력(`~/.gemini/tmp/`)은 유지됨.
		- 안티그래비티와 gemini-cli가 동일 계정 로그인 방식을 쓰면 쿼터를 공유하나, gemini-cli를 별도 API 키(환경 변수)로 연동하면 쿼터 분리 가능.
- **## Troubleshooting**
	- **### Project quota tier unavailable & Quota Exceeded**
		- 현상: API 키는 유효하나 쿼터 등급 인식이 안 되어 사용량이 0으로 차단됨.
		- 원인: AI Studio 프로젝트 매핑 오류 또는 Cloud Billing(결제 정보) 미연결.
		- 해결 1: AI Studio에서 `Create API key in new project` 옵션으로 키를 새로 생성하여 프로젝트 환경을 초기화함.
		- 해결 2 (관리자): Google Admin Console에서 '연령 기반 서비스 제어(18세 이상)' 및 'Gemini 서비스 사용' 설정을 확인하고, Cloud Console에서 결제 계정을 연결함.
- **## log**
	- [[2026-01-03]] Page created.
- **### References**
	- [Google AI Studio API Keys](https://aistudio.google.com/app/apikey)
	- [Google Cloud Console Quotas](https://console.cloud.google.com/iam-admin/quotas)
	- [gemini-cli Documentation](https://geminicli.com)