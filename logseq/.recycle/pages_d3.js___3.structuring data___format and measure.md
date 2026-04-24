date-created:: [[2026-04-21]]
date-updated::
alias::
tags::
ai-sourced:: #in-proofing 
division::
stack::
type::
public:: true

- ## Summary
	-
- ## Steps
	- 원시데이터를 불러오는 일은 일단 [[d3.js/fetch]] 모듈과 하위 메써드에서 알아서 처리한다.
	  logseq.order-list-type:: number
		- dsv 모듈 기반이라면 원시 데이터는 표 형식(tabular format)임을 전제한다. 
		  logseq.order-list-type:: number
		  collapsed:: true
			- [d3-dsv](https://d3js.org/d3-dsv#dsv_parseRows) 공식 문서를 먼저 한 번 읽어라. 아래와 같다.
			- > This module provides a parser and formatter for delimiter-separated values, most commonly [comma-separated values](https://en.wikipedia.org/wiki/Comma-separated_values) (CSV) or tab-separated values (TSV). These tabular formats are popular with spreadsheet programs such as Microsoft Excel, and are often more space-efficient than JSON. This implementation is based on [RFC 4180](http://tools.ietf.org/html/rfc4180).
		- 따라서 첫 줄은 무조건 제목 행이고 내부적으로 JSON 값의 이름이 된다.
		  logseq.order-list-type:: number
		- logseq.order-list-type:: number
		  ```csv
		  technology,count
		  ArcGIS,147
		  D3.js,414
		  Angular,20
		  Datawrapper,171
		  ```
		- 구분자(delimiter)는 바뀔 수 있지만 개행된 줄마다 데이터 한 단위가 있다고 가정한다. 그렇기에 아래 코드에서 각 행을 처리하는 코드를 삽입해 원시데이터에 원하는 서식을 부여할 수 있다.
		  logseq.order-list-type:: number
		- logseq.order-list-type:: number
		  ```js
		  // 원시데이터를 불러온다.
		  // dsv 함수로 불러오는 원시데이터는 표 형식이어야 한다.
		  // dsv 함수는 d3 fetch 모듈의 일부이다.
		  // 해당 모듈은 자바스크립트 Fetch API의 래퍼 함수(warapper function)이다.
		  // 인자로 전달하는 화살표 함수( (d) => {})는 함수 객체이다.
		  // 함수 객체는 불러온 원시데이터의 각 행마다 적용된다.
		  // 따라서 각 행마다 원하는 서식을 적용해 JS 객체로 반환한다. 
		  d3.csv("data/data.csv", (d) => {
		    // ROW CONVERSION
		    // 여기까지는 한줄한줄 정리한다.
		    return {
		      technology: d.technology,
		      count: +d.count,
		    };
		    // 위에서 반환한 JS 객체 (json객체 아님)는
		    // then()으로 연결(chaining)할 때 전달하는 data 배열 객체의 원소가 된다.
		  }).then((data) => {
		    // 여기서 전달하는 data는
		    // 확장된 배열(Extended Array)" 또는 "D3 데이터 배열"이라고 부른다.
		    // ENTIRE DATASET
		    // 여기서부터는 데이터집합 전체를 다룬다.
		  }
		  ```
		- ![image.png](../assets/image_1776913652741_0.png)
		  logseq.order-list-type:: number
			- “Figure 3.14 How and where to load, transform, and measure data in D3” ([Meeks, 2024, p. 83](zotero://select/library/items/VHTGXJRT)) ([pdf](zotero://open-pdf/library/items/FGBNWKIT?page=109&annotation=3SXQVSU7))
			  logseq.order-list-type:: number
	- 아래 코드가 최종 결과물이다. 이를 중심으로 설명한다. 
	  logseq.order-list-type:: number
		- 📁 D:\yonggeun\porter\git\o-m.kr\lab\d3-in-action\03\3.3-Binding_data\started-2025-06-26
		- ```javascript
		  // Append a SVG container
		  const svg = d3
		    .select(".graph")
		    .append("svg")
		    // viewBox는 반드시 지정해야 한다.
		    .attr("viewBox", "0 0 1200 1600");
		  
		  // Load, format and measure the dataset
		  d3.csv("data/data.csv", (d) => {
		    // Format the dataset
		    return {
		      technology: d.technology,
		      count: +d.count,
		    };
		  }).then((data) => {
		    // Log the full dataset
		    console.log("=== full data ===");
		    console.log(data);
		  
		    // How many rows the dataset contains
		    console.log(data.length, " rows"); // => 33
		  
		    // return the min and the max from the given data
		    console.log(
		      "d3.max() -> ",
		      d3.max(data, (d) => d.count),
		    ); // => 1078
		    console.log(
		      "d3.min() -> ",
		      d3.min(data, (d) => d.count),
		    ); // => 20
		    // return an array with min and max of the given data
		    console.log(
		      "d3.extent() -> ",
		      d3.extent(data, (d) => d.count),
		    ); // => [20, 1078]
		  
		    // Sort the data in descending order
		    data.sort((a, b) => b.count - a.count);
		  
		    // Pass the data to another function
		    createViz(data);
		  });
		  
		  // settings
		  const barHeight = 20;
		  const barGap = 2;
		  
		  // Create the bar graph
		  const createViz = (data) => {
		    // empty selection
		    let s = svg.selectAll("rect");
		    // console.log(s);
		    svg
		      .selectAll() // 일단 빈 Selection 객체를 반환해서
		      .data(data) // 거기에 data를 전달하면
		      .join("rect") //
		      .attr("class", (d) => {
		        // console.log(d);
		        return `bar bar-${d.technology}`;
		      })
		      .attr("width", (d) => d.count)
		      .attr("height", barHeight)
		      .attr("x", 0)
		      .attr("y", (d, i) => (barHeight + barGap) * i)
		      .attr("fill", (d) => (d.technology === "D3.js" ? "orange" : "silver"));
		    s = svg.selectAll("rect");
		  };
		  
		  ```
- ## Troubleshooting
	-
- ## log
	- [[2026-04-21]] Page created.
- ### References
	- “3.2.2 Formatting a dataset” ([Meeks, 2024, p. 77](zotero://select/library/items/VHTGXJRT)) ([pdf](zotero://open-pdf/library/items/FGBNWKIT?page=103&annotation=N8A8IPPI))
	- [d3-fetch | D3 by Observable](https://d3js.org/d3-fetch#dsv)
	- [d3-dsv | D3 by Observable](https://d3js.org/d3-dsv#dsv_parseRows)
	- [[d3.js/fetch]]