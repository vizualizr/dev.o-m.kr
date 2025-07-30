## About
	- A journal documenting the process of developing an independent data storytelling blog from scratch
	- ### current stack
		- [[astro]], [[d3.js]], [[tailwindcss]]
		- together with AI agents, [[Copilot]], [[Gemini]], [[Claude]]
- ## Updates
	- query-sort-by:: updated-at
	  query-table:: true
	  query-sort-desc:: true
	  query-properties:: [:page :updated-at]
	  #+BEGIN_QUERY
	  { :query [:find (pull ?p [:block/name :block/updated-at])
	           :where
	           [?p :block/name ?name]
	           [?p :block/updated-at ?updated]
	           (not [?p :page/properties])
	           (not [?p :block/properties])
	           (not [(contains? #{"Start" "contents" "favorites" "recent"} ?name)])]
	   :result-transform (fn [result]
	                       (->> result
	                            (sort-by :block/updated-at >)
	                            (take 20)))}
	  #+END_QUERY
- ### log
	- DONE [[2025-07-30]] The query for fetching the update list has to be updated. >[2025-07-30 12:00 - 12:30](#agenda://?start=1753848006237&end=1753849806237&allDay=false)
	  collapsed:: true
	  :LOGBOOK:
	  CLOCK: [2025-07-23 Wed 08:49:07]--[2025-07-23 Wed 08:49:08] =>  00:00:01
	  :END:
		- [Queries](https://docs.logseq.com/#/page/queries) and [Advanced Queries](https://docs.logseq.com/#/page/advanced%20queries) in Logseq Documentation.
		- If necessary, change the way how it renders result from [this post](https://discuss.logseq.com/t/is-it-possible-to-change-query-output-form-and-what-are-the-syntaxes/22293).
		- See datelog and clojure. Gemini and copilot failed to generate a working code, while Claude succedded!
		- ```clojure
		  #+BEGIN_QUERY
		  {:title "최근 수정된 페이지들 (속성 페이지 제외)"
		   :query [:find (pull ?p [:block/name :block/updated-at])
		           :where
		           [?p :block/name ?name]
		           [?p :block/updated-at ?updated]
		           (not [?p :block/properties])
		           (not [(contains? #{"home" "division" "contents" "favorites" "recent"} ?name)])]
		   :result-transform (fn [result]
		                       (->> result
		                            (sort-by :block/updated-at >)
		                            (take 15)))}
		  #+END_QUERY
		  ```
		- Claude Sonnet 4 solved the problem in 10 minutes, while Gemini, Copilot, and NotebookLM got lost halfway through the dead code.
public:: true
