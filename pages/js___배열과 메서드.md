- [배열과 메서드](https://ko.javascript.info/array-methods)
- ## Methods
	- ### `Arr.map()`
	  id:: 6889e01f-e6c6-4fe8-8e2b-6fcaa1b4ae89
		- array in, then a new array of the elements returned by the given function
		- as stated in the [Array.prototype.map() - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
		- ```js
		  const array1 = [1, 4, 9, 16];
		  
		  // Pass a function to map
		  const map1 = array1.map((x) => x * 2);
		  
		  console.log(map1);
		  // Expected output: Array [2, 8, 18, 32]
		  ```