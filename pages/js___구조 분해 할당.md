- [구조 분해 할당](https://ko.javascript.info/destructuring-assignment)
  title:: js/구조 분해 할당
	- > 객체나 배열을 변수로 '분해’할 수 있게 해주는 구문이다.
	- 배열에서도 쓸 수 있고,
	- ```js
	  // 이름과 성을 요소로 가진 배열
	  let arr = ["Bora", "Lee"]
	  
	  // 구조 분해 할당을 이용해
	  // firstName엔 arr[0]을
	  // surname엔 arr[1]을 할당하였습니다.
	  let [firstName, surname] = arr;
	  
	  alert(firstName); // Bora
	  alert(surname);  // Lee
	  
	  // 아니면 이렇게도 쓸 수 있다.
	  let [firstName, surname] = "Bora Lee".split(' ');
	  // 문자열에서 곧바로 성과 이름을 두 개의 변수에 할당한다.
	  ```
	-
- #### 참고자료
	- [구조 분해 할당 - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#%EA%B0%9D%EC%B2%B4_%EA%B5%AC%EC%A1%B0_%EB%B6%84%ED%95%B4)
- [[js/구조 분해 할당]] #2025-02-07 #DONE ==#once==
  logseq.order-list-type:: number