## About
	- A journal documenting the process of [[developing]] an independent data storytelling blog from scratch.
	- http://dev.o-m.kr
	- ### current stack
		- [[astro]], [[d3.js]], [[tailwindcss]]
		- together with AI agents, [[Copilot]], [[Gemini]], [[Claude]]
- ## Updates
  id:: 691682d3-0523-4306-8742-d3f7f284aaea
	- query-properties:: [:page :date-modified :status]
	  #+BEGIN_QUERY
	  {:title "10 pages recently updated as of today"
	   :query [:find (pull ?p [*])
	           :where
	           ;; 1. ?content에 "date-modified::" 문자열이 포함된 블록 ?b를 찾습니다.
	           [?b :block/content ?content] ; :block/string이 아닌 :block/content를 사용해야 합니다 [1, 2].
	           [(clojure.string/includes? ?content "date-modified::")]
	           
	           ;; 2. 해당 블록 ?b가 속한 페이지 ?p를 찾습니다.
	           [?b :block/page ?p]
	           [?p :block/name _]
	           ]
	   
	   :result-transform (fn [result]
	                       (let [
	                             ;; 페이지에서 날짜 속성 문자열(예: "[[2025-11-13]]")을 추출하는 헬퍼 함수
	                             get-date-string (fn [page]
	                                               ;; 블록 데이터 분석 결과 (대화 기록 참조), 속성 값은 
	                                               ;; :block/properties-text-values 맵에 저장되어 있습니다. [3]
	                                               (let [raw-prop-map (get-in page [:block/properties-text-values])
	                                                     raw-date (get raw-prop-map :date-modified)]
	                                                 (if raw-date
	                                                   raw-date ; [[YYYY-MM-DD]]를 포함한 원본 문자열 그대로 반환
	                                                   "")))]
	                             
	                         ;; 1. 날짜 문자열을 기준으로 오름차순 정렬
	                         (->> result
	                              (sort-by get-date-string) ; :result-transform은 Clojure 함수를 사용하여 정렬합니다 [4, 5].
	                              ;; 2. 내림차순(최신순)으로 뒤집기
	                              reverse
	                              ;; 3. 상위 10개 결과만 선택
	                              (take 10))
	                         )
	   )
	   :collapsed? false
	  }
	  #+END_QUERY
- ### Notes
	- hosted on GitHub Pages with [logseq-SPA action]([[Applying custom domain to GitHub Pages repo]])
- ### Log
	- [[2025-11-13]] Advanced Query in ((691682d3-0523-4306-8742-d3f7f284aaea)) has been updated.
		- To filter the latest article based the user-defined page property, not the native property.
		- See the github issue. [Re-index resets 'created-at' property](https://github.com/logseq/logseq/issues/8556).
	- [[2025-12-16]] Git enabled.
		- Local and remote git repo are enabled.
		- https://github.com/vizualizr/fastlab