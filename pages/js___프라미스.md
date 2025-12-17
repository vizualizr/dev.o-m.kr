date-created:: [[2025-12-08]]
date-modified:: [[2025-12-17]] 
division::
stack::
tags:: 비동기
type::
alias:: js/Promise
public:: true

- ## Summary
	- 자바스크립트 내장 객체로서 비동기 작업의 진행 경과와 결괏값을 표시할 수 있다.
	- 비동기 함수는 항상 Promise 객체를 반환한다. 비동기 작업의 반환값은 Promise 객체를 사용하도록 권장된다.
- ## Steps
	- ### Fundamentals
	  logseq.order-list-type:: number
		- ```js
		  let newPromise = new Promise (function (resolve, reject) {
		    // executor - 실행 처리 부분
		    const isSuccess = Math.random() > 0.5;
		    
		    // 1초 후 실행하는 비동기 작업을 예약
		    // resolve와 reject 함수를 Promise 객체의 상태 변경을 제어한다. 
		    setTimeout(() => {
		      if (isSuccess) {
		        // 성공하면 아래 객체를 선언해 전달한다.
		        resolve({ id: 1, content: "Promise 성공 데이터를 전달합니다." }); 
		      } else {
		        // 실패하면 아래의 Error 객체를 선언해 전달한다.
		        reject(new Error("API 호출에 실패했습니다.")); 
		      }
		    }, 1000);
		  });
		  ```
		- 집행자(executor)는 선언 즉시 처리된다.
		- `resolve`와 `reject`는 콜백의 상태 변화를 선언함과 동시에 콜백이 성공할 경우 혹은 실패할 경우 어떤 인자를 전달할지 결정한다.
		- `resolve()`에 전달한 한 인자는 `then()`이 처리한다.
		- `reject()`에 전달한 인자는 `catch()`이 처리한다.
		- ```js
		  // 따라서 다음과 같이 작성하면
		  // 콜백의 성패에 따라 두 가지 경우 가운데 한 가지를 처리하기에
		  // 실질적으로는 분기문처럼 작동한다.
		  // then()의 반환값은 무조건 Promise 객체이다.
		  
		  newPromise
		    .then((data)=> {
		    	// 콜백 결과가 성공일 경우
		      console.log("Data successfully loaded", data);
		      return data.content;
		    })
		    .catch ((error) => {
		      // 콜백 결과가 실패일 경우
		      console.log(`Error, ${error.message} has occured.`);
		    })
		    .finally (()=> {
		      // 성공 실패와 관계없이 콜백 함수의 실행을 마치면 무조건 실행함
		      console.log("Promise 작업 종료.");
		    })
		  ```
	- Method comparison
	  logseq.order-list-type:: number
		- logseq.order-list-type:: number
		  | 메서드               | 입력 (Input)        | 처리 (Processing)                                                                 | 출력 (Output)                                                                 |
		  |----------------------|---------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------------------|
		  | **Promise.all**      | 여러 Promise 배열   | 모든 Promise가 **성공**해야 함. 하나라도 실패하면 즉시 `reject`.                   | 성공 시: 결과값 배열, 실패 시: 첫 번째 에러로 `reject`                        |
		  | **Promise.allSettled** | 여러 Promise 배열 | 모든 Promise가 끝날 때까지 기다림. 성공/실패 모두 결과에 포함.                     | 결과 객체 배열, `{status:"fulfilled", value:...}` 또는 `{status:"rejected", reason:...}` |
		  | **Promise.race**     | 여러 Promise 배열   | 가장 먼저 완료된 Promise 하나만 결과로 반환. 성공/실패 여부 그대로 반영.            | 첫 번째 완료된 Promise의 결과값 또는 에러                                       |
		  | **Promise.any**      | 여러 Promise 배열   | 가장 먼저 **성공한** Promise 결과 반환. 모든 Promise가 실패하면 `AggregateError`. | 성공 시: 첫 번째 성공 값, 실패 시: 모든 실패를 담은 `AggregateError`          |
	- ### List of JS functions and methods return Promise object
		- | 범주 (Category)        | 함수/메서드 (Function/Method)                                                                 | 설명 (Description) |
		  |------------------------|-----------------------------------------------------------------------------------------------|--------------------|
		  | 네트워크 (Network)     | ==`fetch()`==                                                                                 | HTTP 요청을 보내고 응답을 Promise로 반환 |
		  | Response 객체          | ==`.json()`==, ==`.text()`==, ==`.blob()`==, `.arrayBuffer()`, `.formData()`                  | 응답 본문을 비동기로 파싱 |
		  | Clipboard API          | ==`navigator.clipboard.writeText()`==, ==`navigator.clipboard.readText()`==                   | 클립보드 읽기/쓰기 |
		  | File API               | `File.arrayBuffer()`, ==`File.text()`==                                                       | 파일 내용을 비동기로 읽음 |
		  | File System Access     | `showOpenFilePicker()`, `showSaveFilePicker()`, `FileSystemFileHandle.getFile()`              | 브라우저에서 파일 열기/저장 |
		  | Web Crypto API         | `crypto.subtle.encrypt()`, `crypto.subtle.decrypt()`, `crypto.subtle.sign()`, `crypto.subtle.verify()`<br>`crypto.subtle.digest()`, `crypto.subtle.generateKey()`, `crypto.subtle.importKey()`, `crypto.subtle.exportKey()` | 암호화 관련 작업 |
		  | Streams API            | `ReadableStreamDefaultReader.read()`                                                          | 스트림 읽기 결과를 Promise로 반환 |
		  | Permissions API        | ==`navigator.permissions.query()`==                                                           | 권한 상태 확인 |
		  | Notifications API      | ==`Notification.requestPermission()`==                                                        | 알림 권한 요청 |
		  | Service Workers        | ==`navigator.serviceWorker.register()`==, `navigator.serviceWorker.ready`                     | 서비스 워커 등록/준비 |
		  | Web Bluetooth          | `navigator.bluetooth.requestDevice()`                                                         | 블루투스 장치 요청 |
		  | WebUSB                 | `navigator.usb.requestDevice()`                                                               | USB 장치 요청 |
		  | Web MIDI               | `navigator.requestMIDIAccess()`                                                               | MIDI 접근 요청 |
		  | WebXR                  | `navigator.xr.requestSession()`                                                               | XR 세션 요청 |
		  | IndexedDB (현대화)     | `IDBFactory.open()`은 원래 이벤트 기반이지만, `indexedDB.open()`을 Promise로 래핑한 라이브러리(`idb`)가 널리 사용됨 | DB 접근 |
		- Frequently used functions/methods are highlighted.
- ## Troubleshooting
	- ### `resolve()`와 `reject()`는 왜 Promise 객체의 메서드가 아닌가?
		- #+BEGIN_IMPORTANT
		  일반적인 전역 객체나 함수가 아니다.
		  #+END_IMPORTANT
		- Promise 객체가 선언되면 자바스크립트 런타임이 해당 Promise 객체의 상태를 직접 변경하기 위해 `resolve()`와 `reject()`를 직접 생성한다.
		- 객체 생성과 동시에 상태 관리를 위해 두 개의 은닉 변수(private variable)인 `[[PromiseState]]`, `[[PromiseResult]]`를 내부 상태 저장에 사용한다.
		- 위 두 은닉변수에 접근해 상태를 바꾸는 함수가 `resolve()`와 `reject()`이다.
		- `resolve`와 `reject`는 **클로저(Closure)**의 특성을 이용하여 Executor의 스코프를 넘어, Promise 객체의 **내부 상태**를 영구적으로 참조하고 조작할 수 있다.
		- 이로 인해 Promise 객체의 비동기 상태 관리는 캡슐화가 가능하다.
		- 그럼에도 `resolve()`와 `reject()`가 공개 메서드가 아닌 이유는 Promise 객체의 상태 변화가 오직 executor 맥락에서 단 한번만 허락되어야 하기 때문이다. 만약 사용자가 임의로 Promise 객체의 상태를 변경할 수 있다면 콜백의 독립성, 즉 비공기 작업의 상태 변화에 따른 제어권 위임이 불가능하게 된다.
- ## log
	- [[2025-12-08]] Page created.
	- [[2025-12-17]] Description revised.
		- The guiding sources are added.
		- Sample code added.
		- `resolve()`/`reject()` added.
- ### References
	- [프라미스](https://ko.javascript.info/promise-basics)
	- [📚 자바스크립트 Promise 개념 & 문법 정복하기](https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EB%B9%84%EB%8F%99%EA%B8%B0%EC%B2%98%EB%A6%AC-Promise)
	- [Using promises - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
	- [Promise - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
	- [Using the Fetch API - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
	- [fastlab/js/async/script_new.js at main · vizualizr/fastlab · GitHub](https://github.com/vizualizr/fastlab/blob/main/js/async/script_new.js)
	-
	-