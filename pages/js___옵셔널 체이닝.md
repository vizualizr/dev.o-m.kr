alias:: js/optional chaining
tags::

- [옵셔널 체이닝 '?.'](https://ko.javascript.info/optional-chaining)
- > 내 기준, 최악의 문법이다. 하지만 간편함은 이루 말할 수 없다. 농약같은 지지배.
- 접근하려는 객체에 원하는 속성이 없을 때에도 에러 처리를 별도로 지정하지 않고 안전하게 접근할 수 있다.
- ### 요약 자세한 내용은 [다음](https://ko.javascript.info/optional-chaining#ref-282)을 참조하라.
	- 옵셔널 체이닝 문법 `?.`은 세 가지 형태로 사용할 수 있습니다.
		- `obj?.prop` – `obj`가 존재하면 `obj.prop`을 반환하고, 그렇지 않으면 `undefined`를 반환함
		  logseq.order-list-type:: number
		- `obj?.[prop]` – `obj`가 존재하면 `obj[prop]`을 반환하고, 그렇지 않으면 `undefined`를 반환함
		  logseq.order-list-type:: number
		- `obj?.method()` – `obj`가 존재하면 `obj.method()`를 호출하고, 그렇지 않으면 `undefined`를 반환함
		  logseq.order-list-type:: number
	- 여러 예시를 통해 살펴보았듯이 옵셔널 체이닝 문법은 꽤 직관적이고 사용하기도 쉽습니다. `?.` 왼쪽 평가 대상이 `null`이나 `undefined`인지 확인하고 `null`이나 `undefined`가 아니라면 평가를 계속 진행합니다.
	- `?.`를 계속 연결해서 체인을 만들면 중첩 프로퍼티들에 안전하게 접근할 수 있습니다.
	- `?.`은 `?.`왼쪽 평가대상이 없어도 괜찮은 경우에만 선택적으로 사용해야 합니다.
	- **꼭 있어야 하는 값인데 없는 경우에 `?.`을 사용하면 프로그래밍 에러를 쉽게 찾을 수 없으므로 이런 상황을 만들지 말도록 합시다.**
- #### 시나리오
	- 여러 개의 요소를 가진 객체를 가정하자. 각 요소마다 속성 a와 b가 무작위로 분포한다. 어떤 요소는 속성 a 혹은 속성 b 하나만, 어떤 요소는 둘 다, 또 둘 중 어느 것도 가지지 않은 요소도 있다. 여기서 속성 b만 가진 요소를 걸러내려고 하면 기타 경우의 수에 대한 예외 처리를 모두 해야 한다. 코드가 길어지고 효율도 떨어진다. 그냥 무시하면 되는데 따로 코드를 써야 하니까.
	- ```js
	  // querySelector(...) 호출 결과가 null인 경우 에러 발생
	  let html = document.querySelector('.my-element').innerHTML;
	  
	  // 대안으로 아래처럼 &&를 쓸 수 있는데 코드가 길어지고
	  // 무엇보다 가독성이 떨어진다.
	  let user = {}; // 주소 정보가 없는 사용자
	  alert( user && user.address && user.address.street ); 
	  // undefined, 에러가 발생하지 않습니다.
	  ```
	- 아래처럼 써 보자.
	- ```js
	  let user = {}; // 주소 정보가 없는 사용자
	  alert( user?.address?.street ); // undefined, 에러가 발생하지 않습니다.
	  ```
	- ```js
	  let user = null;
	  alert( user?.address ); // undefined
	  alert( user?.address.street ); // undefined
	  user?.address로 주소를 읽으면 위처럼 user 객체가 존재하지 않더라도 에러가 발생하지 않습니다.
	  ```
	-