date-created:: [[2025-10-16]]
date-updated:: [[2026-05-24]] 
alias::
tags:: 배열
ai-sourced:: [[ai-proofed]] 
division::
stack::
type::
public:: true

- ## Summary
	- 자바스크립트 배열의 값과 구조를 필요에 따라 바꾸기 위해 메서를 알아둘 필요가 있다.
	- d3.js의 경우 함수형 프로그래밍을 권장하며 이에 따라 자료의 불변성을 유지하도록 권장한다. 자료의 값과 구조를 그대로 가시화에 반영하기 때문이다. 불필요한 배열 변경은 가시화된 결과물에 의도치 않은 변화를 초래한다.
	- 따라서 아래 기본 메서를 확인하되 불변성을 유지할 수 있는 방안을 동시에 알아 두어야 한다. 단 자료 정제 과정은 자료와 가시화를 연결하기 전이므로 불변셩을 지키지 않아도 좋다.
- ## Steps
	- ### 기본 메서드
		- #### 원본 배열에서 원소를 추가, 삭제, 변경하는 메서드
			- #+BEGIN_NOTE
			  아래 메서드는 모두 원본 배열을 변경한다. 불변성을 유지하려면 아래 작성한 선언형 구문으로 대체하라.
			  #+END_NOTE
				- `arr.push(...items)`
					- 기존 배열의 끝에 새로운 배열 원소를 하나씩 새로운 원소로 추가한다.
					- `...`는 스프레드 연산자이다. 전개 연산자, 펼침 연산자와 같은 말이다. 아래 코드를 참고하라.
					- ```js
					  items.forEach((item) => {
					    arr.push(item);
					  });
					  ```
				- `arr.pop()`
					- 가장 마지막 원소를 제거한다. 반환값은 제거된 원소이다.
					- ```js
					  let arr = [0, 1, 2 ,3];
					  const popped = arr.pop();
					  console.log(popped);
					  // 3을 출력한다.
					  ```
					- 구문을 달리 하면 다음과 같다.
					- ```js
					  // Array.prototype.length는 getter/setter로 동작하므로
					  // 아래와 같이 쓰면 배열 길이를 하나 줄인다.
					  arr.length = arr.length - 1;
					  console.log(arr);
					  // 출력은 아래와 같다.
					  // [0, 1, 2]
					  ```
				- `arr.shift()`
					- 가장 앞의 원소를 제거한다. 반환값은 제거된 원소이다.
					- ```js
					  let arr1 = [0, 1, 2];
					  
					  // 가장 앞에 있는 원소를 제거한다.
					  const shifted = arr1.shift(); 
					  
					  console.log(`The shifted is ${shifted}`); // 출력: 0 (맨 앞의 값이 나옴)
					  // "The shifted is 0"
					  console.log(`And the array is`);    // 출력: [1, 2] (남은 값들이 앞으로 당겨짐)
					  console.log({arr1});
					  // "And the array is"
					  /*-  
					  // [object Object] 
					  {
					    "arr1": [
					      1,
					      2
					    ]
					  } 
					  -*/
					  ```
				- `arr.unshift(...items)` 선택한 배열 앞에 새로운 원소(들)를 추가한다.
					- ```js
					  let arr1 = [1, 2, 3];
					  
					  console.log(arr1);
					  // 아래를 출력한다.
					  // [1,2,3]
					  
					  const arr1LengthAfterUnshife = arr1.unshift(...[-1, 0]); 
					  console.log(arr1);
					  // 아래를 출력한다.
					  // [-1,0,1,2,3]
					  //
					  console.log(arr1LengthAfterUnshife)
					  // 5
					  ```
		- #### 불변성을 보장하는 메서드
			- [`Array.prototype.slice()`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/slice); 원본 배열에서 일부를 잘라내 반환한다. 따라서 기존 배열에는 변화가 없다.
			  collapsed:: true
				- ```js
				  const animals = ["ant", "bison", "camel", "duck", "elephant"];
				  
				  console.log(animals.slice(2));
				  // Expected output: Array ["camel", "duck", "elephant"]
				  
				  console.log(animals.slice(2, 4));
				  // Expected output: Array ["camel", "duck"]
				  
				  console.log(animals.slice(1, 5));
				  // Expected output: Array ["bison", "camel", "duck", "elephant"]
				  
				  console.log(animals.slice(-2));
				  // Expected output: Array ["duck", "elephant"]
				  
				  console.log(animals.slice(2, -1));
				  // Expected output: Array ["camel", "duck"]
				  
				  console.log(animals.slice());
				  // Expected output: Array ["ant", "bison", "camel", "duck", "elephant"]
				  
				  ```
			- [`Array.prototype.concat()`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/concat); 두 배열을 묶어 새로운 배열을 만들어 반환한다. 마찬가지로 원본 배열에는 변화가 없다.
			  collapsed:: true
				- ```js
				  const array1 = ["a", "b", "c"];
				  const array2 = ["d", "e", "f"];
				  const array3 = array1.concat(array2);
				  
				  console.log(array3);
				  // Expected output: Array ["a", "b", "c", "d", "e", "f"]
				  
				  ```
			- [[js/Array.prototype.map()]]
			  id:: 6889e01f-e6c6-4fe8-8e2b-6fcaa1b4ae89
			- [[js/Array.prototype.filter()]]
			  id:: 6a018ba7-827c-4f1c-964d-fcbb7fe3ae3c
- ## Troubleshooting
	- ### 원본 배열을 변경하는 메서드 목록과 이를 대체하는 선언형 코드
		- 배열 메서드는 원본 배열을 변경한다. 따라서 배열의 [[불변성]]을 유지하는 동시에 원하는 값과 구조를 얻기 위해 다음 방법을 사용하라.
		- ```js
		  const items = [0, 1, 2, 3, 4, 5]
		  
		  // ---------------
		  // push()
		  // ---------------
		  const newItems = ['a', 'b']
		  const pushed = [...items, ...newItems];
		  
		  // ---------------
		  // pop()
		  // ---------------
		  // 음수 인덱스는 배열의 끝부터 세기 시작한다.
		  // 즉 -1은 끝에서 첫 번째 원소다.
		  const itemsAfterPop = items.slice(0, -1);
		  console.log(itemsAfterPop)
		  
		  // ---------------
		  // shift()
		  // ---------------
		  const itemsAfterShift = items.slice(1);
		  console.log(itemsAfterShift)
		  
		  // ---------------
		  // unshift()
		  // ---------------
		  const addition = ['a', 'b']
		  const itemsUnshifted = [...addition, ...items]
		  console.log(itemsUnshifted);
		  
		  // ---------------
		  // splice()
		  // ---------------
		  // splice()를 활용한 injection의 경우
		  const injection = ['a', 'b', 'c']
		  const injected = [
		    ...items.slice(0, 3),
		    ...injection,
		    ...items.slice(3)
		  ]
		  
		  // 원본을 다시 확인하면 변함이 없다.
		  console.log({items})
		  
		  // ---------------
		  // sort()
		  // ---------------
		  const arrayToSort = [1, 30, 4, 21, 100000];
		  // 배열 안의 자료형은 무시하고 utf-16 문자열로 변환해 비교한다.
		  const sortedAsIs = [...arrayToSort].sort();
		  console.log(sortedAsIs);
		  // 따라서 결괏값은 아래와 같다.
		  // [1, 100000, 21, 30, 4]
		  //
		  // number로 비교하려면 아래처럼 형변환 해야 한다.
		  // 현재는 내림차순이다.
		  const sortedAsNumber = [...arrayToSort].sort((prev, next) => (+next - +prev));
		  console.log(sortedAsNumber);
		  // 아래를 출력한다.
		  // [100000,30,21,4,1]
		  
		  // reverse()
		  const reversed = [...arrayToSort].reverse();
		  console.log(`${arrayToSort} is reversed to ${reversed}`);
		  
		  // fill() 해당 배열의 원소를 한 값으로 모두 채운다.
		  const filled = [...arrayToSort].fill(0);
		  console.log(`${arrayToSort} is filled as ${filled}`);
		  
		  // copyWithin() 지정된 위치에 지정된 값을 채운다.
		  const copiedWithin = [...arrayToSort].copyWithin(0, 2, 4);
		  console.log(`${arrayToSort} is partially replaced as ${copiedWithin}`);
		  
		  // 원본 유지 확인
		  console.log(`The source array is immutable as shown, ${arrayToSort}`);
		  ```
		- [[자바스크립 배열 연산을 변환, 선별, 압축으로 구분해 함수형 프로그래밍으로 처리하는 방법]]
	- ### 예제들
		- 배열에서 중복을 제거한 후 다시 반환하는 코드이다. 자세한 내용은 [예제](https://ko.javascript.info/task/array-unique)를 참고하라.
			- ```js
			  // indexOf는 해당 원소가 출현하는 첫 색인을 반환한다.
			  // 현재 확인하고 있는 원소의 색인(index), 그리고 이 원소를 검색한 결과인 indexOf의 색인이 같다면
			  // 해당 원소가 배열의 가장 처음에 출현한 상태이다.
			  // 따라서 결과는 참이고 array.filter가 반환할 배열에 추가된다.
			  // 반면 현재 확인하고 있는 원소의 색인(index), 그리고 이 원소를 검색한 indexOf의 색인이 다르다면
			  // 해당 원소는 현재 index에 앞서 이미 존재한다는 의미이고 결괏값에 추가할 필요가 없다.
			  // 따라서 false를 반환하고 결과에서 제거한다.
			  
			  // 시간 복잡도는 ($O(N^2)$)이다.
			  
			  const unique = (arr) => {
			    return arr.filter((item, index) => index === arr.indexOf(item));
			  }
			  
			  const strings = [
			    "Hare",
			    "Krishna",
			    "Hare",
			    "Krishna",
			    "Krishna",
			    "Krishna",
			    "Hare",
			    "Hare",
			    ":-O"
			  ];
			  
			  console.log(unique(strings))
			  // ["Hare","Krishna",":-O"]
			  ```
			- | **배열의 크기 (N)** | **기존 filter + indexOf (O(N2))** | **최적화 Set + ... (O(N))** | **성능 차이** |
			  | ---- | ---- | ---- |
			  | $1,000$ 개 (천 개) | $1,000,000$ 번 (백만) | **$2,000$ 번** (이천) | 약 500배 고속 |
			  | $10,000$ 개 (만 개) | $100,000,000$ 번 (1억) | **$2,000s$ 번** (2만) | 약 5,000배 고속 |
			  | $100,000$ 개 (십만 개) | $10,000,000,000$ 번 (**100억**) ➔ *브라우저 먹통* | **$200,000$ 번** (20만) | **약 50,000배 고속** |
			- 즉 `filter`, `indexOf()` 조합은 시간 복잡도가 $O(N^2)$이므로 입력값의 제곱에 비례하는 시간이 필요한 반면, `Set`으로 작성한 구문의 시간 복잡도는 $O(N)$이므로 입력값에 정비례하는 시간이 필요하다.
			- 아래는 `Set`을 이용한해법이다. 자세한 내용은 [Set]([[js/맵과 셋]])을 참고하라.
			- ```js
			  // Set은 중복을 자동으로 걸러내는 자료형이므로
			  // 배열을 풀어 Set으로 저장한 뒤
			  // 다시 배열로 묶으면 중복값이 자동으로 제거된다.
			  
			  // 시간 복잡도는 ($O(N)$)이다.
			  
			  const unique = (arr) => [...new Set(arr)];
			  
			  console.log(unique(strings)); // ["Hare", "Krishna", ":-O"]
			  ```
		- 배열 원소의 순서를 무작위로 뒤섞어야 할 때. 자세한 내용은 해당 [예제](https://ko.javascript.info/task/shuffle)를 참고하라.
			- 내가 작성한 답변은 아래와 같다.
			- ```js
			  const getRandom = (num) => Math.floor(Math.random() * Math.abs(num));
			  
			  const shuffle = (items) => {
			    let iteration = items.length
			    for (let i = 0; i < iteration; i++) {
			      let remainedLength = items.length - i;
			      
			      let spliced = items.splice(getRandom(remainedLength), 1);
			      // console.log("spliced ", spliced);
			      // console.log("items ", items);
			      items.push(...spliced);
			    }
			    // console.log('result ', items)
			  }; //
			  
			  const counts = {};
			  for (let i = 0; i < 100000; i++) {
			    let a = [1,2,3];
			    shuffle(a);
			    counts[a.join('')] = (counts[a.join('')] || 0) + 1;
			  }
			  console.log(counts);
			  
			  //
			  
			  ```
			- 해법이 절차적이다. 따라서 시간복잡도는 입력값의 제곱에 비례한다. $$O(N^2)$$
			- 아래는 피셔-예이츠 셔플(Fisher-Yates shuffle) 알고리즘이다. 시간복잡도는 입력값에 정비례한다. $$O(N)$$
			- ```js
			  // 피셔-예이츠 셔플 (Fisher-Yates Shuffle)
			  // 가장 빠르게 배열을 무작위로 섞는 방법이다.
			  
			  const shuffle = (items) => {
			    // 배열의 끝에서 시작한다.
			    for (let i = items.length - 1; i > 0; i--) {
			      
			      // 현재 범위 안에서 무작위로 색인 하나를 뽑는다.
			      const j = Math.floor(Math.random() * (i + 1));
			      
			      // 현재 순회 중인 색인과 무작위로 뽑은 색인을 맞바꾼다. 
			      // 맞바꾸는 방식은 구조분해 할당이다.
			      [items[i], items[j]] = [items[j], items[i]];
			    }
			  };
			  
			  // ----------------------------------------------------
			  // 몬테카를로 시뮬레이션 (확률 검증)
			  // ----------------------------------------------------
			  const counts = {};
			  
			  for (let i = 0; i < 100000; i++) {
			    let a = [1, 2, 3];
			    shuffle(a);
			    counts[a.join('')] = (counts[a.join('')] || 0) + 1;
			  }
			  
			  console.log(counts);
			  ```
			- 실제 알고리즘의 작동 방식은 피셔-예이츠 셔플 항목에서 [현대적인 방법](https://ko.wikipedia.org/wiki/%ED%94%BC%EC%85%94-%EC%98%88%EC%9D%B4%EC%B8%A0_%EC%85%94%ED%94%8C#%ED%98%84%EB%8C%80%EC%A0%81%EC%9D%B8_%EB%B0%A9%EB%B2%95)을 확인하라.
			- 요약한 그림은 아래와 같다.
			- | Range | Roll | Scratch | Result |
			  | 1–6 | 6 | A G C D E | **H** B F   |
			  | 1–5 | 1 | **E** G C D | **A** H B F   |
			  | 1–4 | 3 | E G **D** | **C** A H B F   |
			  | 1–3 | 3 | E G | **D** C A H B F   |
			  | 1–2 | 1 | **G** | **E** D C A H B F   |
		-
- ## log
	- [[2026-05-23]] Page created.
	- [[2026-05-23]] 불변성을 보장하는 선언형 구문 추가함.
	- [[2026-05-24]] 예제 코드 정리 마침.
- ### References
	- 제일 먼저 [배열과 메서드의 마지막 요약](https://ko.javascript.info/array-methods#ref-256)에서 자바스크립트의 배열 메서드로 가능한 작업의 목록을 확인하라.
	- 개별 메서드의 구체적은 사항은 아래 세 문서에처 출발해 각 메서드로 수행하는 작업을 숙독하라.
		- [Array - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array)
		- [배열과 메서드](https://ko.javascript.info/array-methods)
		- [얕은 복사 - MDN Web Docs 용어 사전: 웹 용어 정의 | MDN](https://developer.mozilla.org/ko/docs/Glossary/Shallow_copy)