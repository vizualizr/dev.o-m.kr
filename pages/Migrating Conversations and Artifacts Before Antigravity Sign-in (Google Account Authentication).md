date-created:: [[2026-01-23]]  
date-modified:: [[2026-01-23]]  
division:: [[makr]]  
stack:: frontend  
tags:: google-auth, account-migration, antigravity-memory, backup-brain, troubleshooting  
type::  
alias::  
public:: true  
status:: [[ai-generated]]

- ## Summary
	- Antigravity IDE에서 Google 계정 변경 시 발생하는 대화 및 기억(Artifacts) 유실 문제를 분석하고, 이를 방지하기 위한 이주 전략(Backup & Restore)을 정리함. 계정 변경은 단순 로그아웃이 아닌 '환경의 단절'을 의미하므로 사전 백업이 필수적임.
- ## Steps
	- #+BEGIN_EXAMPLE
	  # Backup Brain Artifacts
	  
	  Run this PowerShell command to back up the agent's brain artifacts (task list, plans, guides) to your local project folder `.agent/brain_backup`. This allows you to commit them to Git.
	  
	  ```powershell
	  $source = "C:\Users\<USERNAME>\.gemini\antigravity\brain\<NUMERICALID>"
	  $dest = ".agent/brain_backup"
	  New-Item -ItemType Directory -Force -Path $dest
	  Copy-Item -Path "$source\*" -Destination $dest -Recurse -Force
	  Write-Host "Backup complete to $dest"
	  ```
	  # Restore Brain Artifacts
	  **WARNING**: This will overwrite the current agent memory with the backup.
	  
	  ```powershell
	  $source = ".agent/brain_backup"
	  $dest = "C:\Users\<USERNAME>\.gemini\antigravity\brain\<NUMERICALID>"
	  Copy-Item -Path "$source\*" -Destination $dest -Recurse -Force
	  Write-Host "Restore complete from $source"
	  ```
	  #+END_EXAMPLE
- ## Troubleshooting
	- **문제**: 단순히 계정을 변경할 경우 진행 중이던 작업 계획(`task.md`)이나 구현 계획(`implementation_plan.md`)을 에이전트가 잊어버리는 현상 발생.
		- **유실 범위 분석**:
			- **대화 내역 (Chat History)**: 세션 기반이므로 계정 변경 시 [완전 단절].
			- **단기 기억 (Brain Artifacts)**: [task.md](cci:7://file:///C:/Users/onlin/.gemini/antigravity/brain/c2d3e2cb-768f-40b0-a80a-a8e0b318d6c2/task.md:0:0-0:0) 등이 저장된 Brain 폴더는 계정별 고유 ID를 사용하므로 [접근 불가].
			- **프로젝트 파일 (Source Code)**: 로컬 파일(`.agent` 포함)은 유지되나, 에이전트의 맥락 인식은 초기화됨.
	- **해결**: 'Brain Backup' 워크플로우를 활용해 기억을 이삿짐 싸듯 파일로 변환하여 계정 간 이동 시 맥락을 보존하는 절차 확립.
		- **이주(Migration) 전략 수립**:
			- **백업 (Before Logout)**: 현재 계정에서 `/backup_brain` 명령을 실행하여 Brain Artifacts를 `.agent/brain_backup`으로 추출.
			- **복원 (After Login)**: 새 계정 로그인 후 백업된 아티팩트를 새 Brain 폴더로 복사하여 작업 맥락(Context)을 강제로 주입.
- ## log
	- [[2026-01-23]] Analyzed account migration impact and documented backup strategy.
- ### References
	-
- ---
- ## Summary
	- A solution to avoid the loss of conversations and memory (Artifacts) when changing Google accounts in Antigravity IDE, and a summary of migration strategies (Backup & Restore) to prevent it.
	- Account change means not just a simple logout but a ‘disconnection of environment,’ so pre-backup is essential.
- ## Steps
	- ### copy and paste the below as a workflow in Antigravity
		- #+BEGIN_EXAMPLE
		  # Backup Brain Artifacts
		  
		  Run this PowerShell command to back up the agent's brain artifacts (task list, plans, guides) to your local project folder `.agent/brain_backup`. This allows you to commit them to Git.
		  
		  ```powershell
		  $source = "C:\Users\<USERNAME>\.gemini\antigravity\brain\<NUMERICALID>"
		  $dest = ".agent/brain_backup"
		  New-Item -ItemType Directory -Force -Path $dest
		  Copy-Item -Path "$source\*" -Destination $dest -Recurse -Force
		  Write-Host "Backup complete to $dest"
		  ```
		  # Restore Brain Artifacts
		  **WARNING**: This will overwrite the current agent memory with the backup.
		  
		  ```powershell
		  $source = ".agent/brain_backup"
		  $dest = "C:\Users\<USERNAME>\.gemini\antigravity\brain\<NUMERICALID>"
		  Copy-Item -Path "$source\*" -Destination $dest -Recurse -Force
		  Write-Host "Restore complete from $source"
		  ```
		  #+END_EXAMPLE
- ## Troubleshooting
	- **Issue**: Simply changing accounts causes the agent to forget ongoing work plans (`task.md`) or implementation plans (`implementation_plan.md`).
		- **Loss Scope Analysis**:
			- **Conversation History (Chat History)**: Session-based, so account change results in [complete disconnection].
			- **Short-term Memory (Brain Artifacts)**: Files such as task.md [( in Bing)](https://www.bing.com/search?q="cci%3A7%3A%2F%2Ffile%3A%2F%2F%2FC%3A%2FUsers%2Fonlin%2F.gemini%2Fantigravity%2Fbrain%2Fc2d3e2cb-768f-40b0-a80a-a8e0b318d6c2%2Ftask.md%3A0%3A0-0%3A0") stored in the Brain folder use account-specific unique IDs, thus [inaccessible].
			- **Project Files (Source Code)**: Local files (including `.agent`) are preserved, but the agent’s contextual awareness is reset.
	- **Solution**: Use the ‘Brain Backup’ workflow to convert memory into files like packing for a move, thereby establishing a procedure to preserve context during account migration.
		- **Migration Strategy Establishment**:
			- **Backup (Before Logout)**: Execute the `/backup_brain` command in the current account to extract Brain Artifacts into `.agent/brain_backup`.
			- **Restore (After Login)**: After logging into the new account, copy the backed-up artifacts into the new Brain folder to forcibly inject the work context.
- ## log
	- [[2026-01-23]] Analyzed account migration impact and documented backup strategy.
- ### References
	-