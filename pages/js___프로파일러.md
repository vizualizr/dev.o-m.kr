alias:: js/profiler

- ## 입력
  id:: 68f6ed87-6012-42e6-9a5b-a24e003a6218
	- [[js/인터프리터]]가 바이트코드를 실행하는 과정에서 생성하는 실시간 원시 데이터
- ## 동작
  id:: 68f6efbb-6df7-4c3b-bd24-862047032c51
	- ==[[js/프로파일러]]는 인터프리터가 생성하는 원시 데이터를 수집해 최적화의 바탕이 되는 실행 통계(execution statastics)를 작성한다.==
	  logseq.order-list-type:: number
	  id:: 68f9df3b-f810-487d-8e1a-26d1163ff67e
		- 이때 최적화가 필요한 뜨거운 함수(hot function)을 식별한다.
		  logseq.order-list-type:: number
		- 코드를 감시하며 함수의 호출 빈도, 사용된 인자의 자료형 드을 바탕으로 프로파일링 데이터를 수집한다.
		  logseq.order-list-type:: number
		- 수집 데이터를 바탕으로 뜨거운 함수를 식별한다. 뜨거운 함수는 반복 실행되기에 최적화가 필요한 함수다.
		  logseq.order-list-type:: number
- ## 출력
  id:: 68f7017a-a4a6-4d2a-a7a3-b95b91f80c12
	- 최적화 요청을 전송한다.
	  id:: 68f71c79-3f1c-4e80-99d9-7ca8f3712cc6
	- 최적화 프로파일(optimization profile)이라는 보고서를 함께 제출한다.