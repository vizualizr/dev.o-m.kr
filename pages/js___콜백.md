date-created:: [[2025-12-08]]
date-modified:: [[2025-12-08]]
division::
stack::
tags::
type::
alias::
public:: true

- ## Summary
	- #+BEGIN_NOTE
	  기다려, 지금 하는 거 먼저 처리한 다음에 널 부를께.
	  #+END_NOTE
	- 함수 A가 함수 B를 인수로 전달 받아 실행한다면 함수 B는 A의 콜백 함수이다.
	- 이는 함수 B가 반드시 함수 A에서 지정한 시점에 실행하도록 보장한다.
- ## Steps
	- 다음 예를 참고하라. [출처](https://ko.javascript.info/callbacks)
	- ```js
	  // 스크립트를 불러온다.
	  function loadScript(src, callback) {
	    let script = document.createElement('script');
	    script.src = src;
	    
	    // 콜백을 지정한다.
	    // 여기서는 불러오기를 완료했을 때 하나
	    script.onload = () => callback(script);
	    // 그리고 에러 발생 시 하나
	    // 총 두 개의 콜백을 지정했다.
	    script.onerror = () => callback(new Error (`${src}를 불러오는 과정에서 에러가 발생했습니다.`));
	    
	    // 브라우저는 페이지에 스크립트가 추가될 경우 불러오기를 완료하면 자동으로 실행한다.
	    // 따라서 아래처럼 append만 해도 브라우저가 불러온 스크립트를 바로 실행한다.
	    document.head.append(script);
	  }
	  
	  // 위처럼 선언한 후 아래와 같이 사용한다.
	  loadScript('/my/script.js', function(error, script) {
	    if (error) {
	      // 에러 처리
	    } else {
	      // 스크립트 로딩이 성공적으로 끝남
	    }
	  });
	  ```
- ## Troubleshooting
	-
- ## log
	- [[2025-12-08]] Page created.
- ### References
	- [자바스크립의 콜백 함수 – 자바스크립트에서 콜백 함수가 무엇이고 어떻게 사용하는지 알아봅시다](https://www.freecodecamp.org/korean/news/https-www-freecodecamp-org-news-javascript-callback-functions-what-are-callbacks-in-js-and-how-to-use-them/)