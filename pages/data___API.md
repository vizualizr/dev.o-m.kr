date-created:: [[2026-05-14]]
date-updated:: [[2026-05-14]]
alias::
tags::
ai-sourced:: 
division::
stack::
type::
public:: true

- ## Summary
	-
- ## Steps
	-
- ## Troubleshooting
	-
- ## log
	- [[2026-05-14]] Page created.
- ### References
	- 음악 분석 API #ai-generated
		- | 서비스 및 API 이름 | 기능적 특징 | 무료 여부 (Pricing) |
		  | :--- | :--- | :--- |
		  | **Track Analysis API by SoundNet** | 곡 제목과 아티스트 이름만으로 Key, Tempo, Mode 등을 반환하며, 기존 스포티파이 API와 가장 유사하여 대체제로 가장 많이 추천됩니다. | **기본 무료 제공** (일부 제한 제공 후, 상위 요청량 필요 시 월 유료 플랜 가입 필요). |
		  | **Spotify Extended Audio Features API** | 스포티파이의 기존 요청 및 응답 형식을 그대로 모방하여 구현된 드롭인(Drop-in) 형태의 인프라 API입니다. | **유료 기반** (RapidAPI 플랫폼을 통한 쿼타별 구독 요금제 적용). |
		  | **Essentia.js / Essentia** | 오픈소스 오디오 신호 분석 라이브러리입니다. 30초 미리듣기 음원 파일 등을 활용해 로컬 환경에서 직접 오디오 특징을 추출합니다. | **100% 완전 무료** (서버 비용이나 API 제한이 없는 오픈소스 오픈 데이터). |
			- 음악 재생기의 가시화 모듈은 대부분 오디오 신호를 나눈 뒤 FFT알고리즘으로 고음, 중음, 저음의 에너지 크기를 측정하는 방식이다.
			- 반면 위 분석 API는 음의 연결 상태 등을 기본으로 곡 단위에서 구조, 템포(BPM), AI 기반의 고차원 맥락(분위기, 어울리는 맥락) 등을 제시할 수 있다.
			- Essentia 는 클라이언트 사이드로 구동 가능. 맥북 에어 2013에서 서비스로도 구동 가능.
			- [Spotify에서 제공하던 동일한 기능의 API](https://developer.spotify.com/documentation/web-api/reference/get-audio-analysis)는 `deprecated`임.