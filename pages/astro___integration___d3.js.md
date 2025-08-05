tags:: d3.js

- date-created:: [[2025-07-31]]
  date-modified::
  division:: [[frontend]] 
  stack::
  tags:: [[astro]] 
  type::
  public:: true
- ## Summary
	- No itegration has been listed on official astro website.
- ## Steps
	- #### d3.js in component
	  logseq.order-list-type:: number))
		- ##### client-side JavsScript
		  logseq.order-list-type:: number))
			- [Template directives reference | Docs](https://docs.astro.build/en/reference/directives-reference/#isinline
			  logseq.order-list-type:: number)))
				- logseq.order-list-type:: number))
				  #+BEGIN_IMPORTANT
				  Add the directive, `is:inline`, when you want to run d3.js code as a client-side script.
				  #+END_IMPORTANT
				- logseq.order-list-type:: number))
				  ```html
				  <div class="h-max block">
				      <svg id="frame" width="640" xmlns="http://www.w3.org/2000/svg">
				          <g class="chart fill-lime-500 opacity-50"> </g>
				      </svg>
				  </div>
				  
				  <!-- Since this is a client-side script, the `is:inline` directive must be included. -->
				  <!-- Without it, you may need to import every function from each file individually. -->
				  <!-- For more details, refer to [Astro's official directive reference] -->
				  <!-- (https://docs.astro.build/reference/directives-reference/#isinline). -->
				  <script is:inline src="https://d3js.org/d3.v7.min.js"></script>
				  
				  <script is:inline src="/src/assets/script/chart/config.js"></script>
				  <script is:inline src="/src/assets/script/chart/layout.js"></script>
				  <script is:inline src="/src/assets/script/chart/update.js"></script>
				  <script is:inline src="/src/assets/script/chart/main.js"></script>
				  ```
			- [Scripts and event handling](https://docs.astro.build/en/guides/client-side-scripts/)
			  logseq.order-list-type:: number)
			- For other integrations, follow [the integration installing guide](https://docs.astro.build/en/guides/framework-components/#installing-integrations)
			  logseq.order-list-type:: number))
		- ##### styling
		  logseq.order-list-type:: number
			- You can assign a class attribute to an SVG tag, allowing you to apply CSS in the same way as with HTML tags.
			  logseq.order-list-type:: number))
			- External styles can be specified using the following method:
			  logseq.order-list-type:: number))
				- [Styles and CSS | Docs](https://docs.astro.build/en/guides/styling/#external-styles)
				  logseq.order-list-type:: number)))))
- ### Key references (KO)
  collapsed:: true
	- #### d3.js in component
	  logseq.order-list-type:: number))
		- ##### client-side JavsScript
		  logseq.order-list-type:: number))
			- [템플릿 지시어 참조 | Docs](https://docs.astro.build/ko/reference/directives-reference/#isinline)
			  logseq.order-list-type:: number))
				- logseq.order-list-type:: number))
				  #+BEGIN_IMPORTANT
				  d3.js는 프론트엔드 프레임워크이므로 만약 astro 컴포넌트에 클라이언트즉 스크립트를 삽입하고 싶다면 `<script>` 태그에 `is:inlne`을 추가하라.
				  #+END_IMPORTANT
				- logseq.order-list-type:: number))
				  ```html
				  <div class="h-max block">
				      <svg id="frame" width="640" xmlns="http://www.w3.org/2000/svg">
				          <g class="chart fill-lime-500 opacity-50"> </g>
				      </svg>
				  </div>
				  
				  <!-- 클라이언트 스크립트 이므로 is:inline을 삽입한다. -->
				  <!-- 이를 삽입하지 않으면 각 파일의 함수를 전부 import로 불러와야 한다. -->
				   <!-- 자세한 내용은 https://docs.astro.build/ko/reference/directives-reference/#isinline 를 참조하라. -->
				  <script is:inline src="https://d3js.org/d3.v7.min.js"></script>
				  
				  
				  <script is:inline src="/src/assets/script/chart/config.js"></script>
				  <script is:inline src="/src/assets/script/chart/layout.js"></script>
				  <script is:inline src="/src/assets/script/chart/update.js"></script>
				  <script is:inline src="/src/assets/script/chart/main.js"></script>
				  ```
			- [UI 구축 > 스크립트 및 이벤트 처리 | Docs](https://docs.astro.build/ko/guides/client-side-scripts/#script-processing)
			  logseq.order-list-type:: number)
			- [프런트엔드 프레임워크 | Docs](https://docs.astro.build/ko/guides/framework-components/#installing-integrations)
			  logseq.order-list-type:: number))
		- ##### styling
		  logseq.order-list-type:: number))
			- SVG 태그에 클래스 속성 지정이 가능하므로 HTML 태그와 동일한 방법으로 CSS를 적용할 수 있다.
			  logseq.order-list-type:: number))
			- 다음 방법에 따라 외부 스타일을 지정한다.
			  logseq.order-list-type:: number))
				- [스타일 및 CSS | Docs](https://docs.astro.build/ko/guides/styling/#%EC%99%B8%EB%B6%80-%EC%8A%A4%ED%83%80%EC%9D%BC)
				  logseq.order-list-type:: number)))
- ## log
	- [[2025-07-31]] Page created.
- ### References
	-