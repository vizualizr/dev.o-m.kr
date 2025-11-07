- #+BEGIN_QUOTE
  원문읽기 [나머지 매개변수와 전개 구문](https://ko.javascript.info/rest-parameters-spread)
  #+END_QUOTE
- ### [나머지 매개변수와 전개 구문](https://ko.javascript.info/rest-parameters-spread#spread-syntax)
	- #### 나머지 매개변수로서
		- 시나리오 1-인수가 넘어오는데 배열 비스무리하게 연속된 값이다. 하지만 몇 개가 올지는 모른다면?
		- 이럴 때 넘어오는 인수를 모아서 전달할 수 있다.
		- ```js
		  function showName(firstName, lastName, ...titles) {
		    alert( firstName + ' ' + lastName ); // Bora Lee
		  
		    // 나머지 인수들은 배열 titles의 요소가 됩니다.
		    // titles = ["Software Engineer", "Researcher"]
		    alert( titles[0] ); // Software Engineer
		    alert( titles[1] ); // Researcher
		    alert( titles.length ); // 2
		  }
		  
		  // 세 개 이상이면 일단 함수는 실행이 된다.
		  // 임의의 갯수로 인수를 전달할 수 있다.
		  showName("Bora", "Lee", "Software Engineer", "Researcher");
		  ```
	- #### 전개 구문으로서 (스프레드 구문)
		- **배열을 통째로 인수로 넘겨주는 방법**이다. 전개구문이라고도 한다.
		- 반복 가능한 변수형의 개별 요소를 인수로 전달한다.
			- 배열, 객체 등 반복가능한 변수형(iterable)에서 사용할 수 있다.
		- ```js
		  // 최대값을 반화하는 함수 아래처럼 5를 반환한다.
		  alert( Math.max(3, 5, 1) ); // 5
		  
		  let arr = [3, 5, 1];
		  alert( Math.max(arr) ); 
		  // NaN
		  // Math.max의 인수는 배열이 아닌 숫자의 목록이다.
		  // 아래와 같다.
		  // https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math/max
		  Math.max()
		  Math.max(value1)
		  Math.max(value1, value2)
		  Math.max(value1, value2, /* …, */ valueN)
		  //따라서 오류를 출력한다.
		  
		  // ...arr은 전개 구분이다. 즉 해당 배열에 있는 변수를 인수 목록으로 변환해 전달한다.
		  alert( Math.max(...arr) ); // 5 (전개 구문이 배열을 인수 목록으로 바꿔주었습니다.)
		  // 원하는 값이 나온다.
		  ```
		- 다음과 같이 활용할 수 있다.
		- ```js
		  let arr1 = [1, -2, 3, 4];
		  let arr2 = [8, 3, -8, 1];
		  
		  alert( Math.max(...arr1, ...arr2) ); // 8
		  // 그 자체로 인수의 묶음과 동일하니 여러 개를 전달해도 되고,
		  
		  let arr1 = [1, -2, 3, 4];
		  let arr2 = [8, 3, -8, 1];
		  
		  alert( Math.max(1, ...arr1, 2, ...arr2, 25) ); // 25
		  // 다른 인수를 추가해도 된다. 그냥 하나의 인수 집합이니까. 
		  // 배열과는 다르다. 배열과는.
		  
		  // 인수를 받는 함수를 반복실행하게 된다. 
		  ```
		- 배열 복사도 가능하다. 반복 가능한 자료형에 사용 가능하니 객체 복사 또한 가능하다.
		- ```js
		  let arr = [1, 2, 3];
		  let arrCopy = [...arr]; // 배열을 펼쳐서 각 요소를 분리후, 매개변수 목록으로 만든 다음에
		                          // 매개변수 목록을 새로운 배열에 할당함
		  ```