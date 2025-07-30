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
- [More information on this page.]([[dev.o-m.kr]])