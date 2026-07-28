date-created:: [[2026-07-14]]
date-updated:: [[2026-07-14]]
alias:: vizualization/tools
tags::
ai-sourced:: 
division::
stack::
type::
public:: true

- ## Summary
	- A list of viable tools for visualization
- ## Steps
	- visualization / for all in one approach to generate visualizations
		-
		- [[d3.js]]
			- 최종 결과물이 갖는 시각적 복잡성을 이미 존재하는 차트 형식으로 구현할 수 없을 때 필요한 도구다.
			- 반대로 말하면 기존에 존재하는 시각적 문법으로 해결 가능한 상황이라면 굳이 d3.js를 쓸 필요가 없다.
		- [RAWGraphs](https://www.rawgraphs.io/)
			- The website provides [an intuitive test tool](https://app.rawgraphs.io/) to align your data onto the traditional charting schemes. In case you need to verify your chart this is the shortcut.
		- [visx from AirBnB](https://visx.airbnb.tech/), and [the docs](https://visx.airbnb.tech/docs)
		- [Vega](https://vega.github.io/vega/)
	- Wrangling & cleaning / 데이터 정제 도구가 따로 있다.
		- [tidy.js](https://pbeshai.github.io/tidy/), [tidy.js repo](https://github.com/pbeshai/tidy)
		- [GitHub - uwdata/arquero: Query processing and transformation of array-backed data tables. · GitHub](https://github.com/uwdata/arquero)
- ## Troubleshooting
	- [A GeekNews post](https://news.hada.io/topic?id=14866) discussing the current web stack for visualization [[2026-07-14]]. [Original Post](https://news.ycombinator.com/item?id=40378791) | [Mike Bostock's post on observablehq.com](https://observablehq.com/@mbostock/10-years-of-open-source-visualization)
		- post is outdated, as it is on 2025-05-18
		- d3.js가 완벽한 도구라 할 수 없다. 대신 추상화 수준이 높은 건 사실이다. 단 이 높은 추상화 수준과 생산성 사이에 충돌이 있는 건 사실이다. Observable Plot이 중간 매개 역할을 할 수 있겠지만 생산성 외에 다른 장점이 무엇인가라는 질문에는 논란의 여지가 있다.
		- 다만 커뮤니티 자체의 성격때문인지 글의 성향이 대부분 개발자 중심이며 창의적 가시화보다는 정통 차트를 중심으로 논하고 있다고 생각함.
		- 따라서 창의적인 측면, 혹은 디자인이 갖는 차별성을 더 중요하게 여기는 팀이나 개발자라면 이 포스트의 다양한 의견을 걸러서 들을 필요가 있음.
		- 이를테면 Mike Bostock은 [데이터 가시화 작업의 80%가 데이터 자체를 만지는 작업](https://news.hada.io/topic?id=3789#:~:text=%EB%8C%80%EB%B6%80%EB%B6%84%EC%9D%98%20%EA%B2%BD%EC%9A%B0%2C%20%EC%8B%9C%EA%B0%81%ED%99%94%20%EC%9E%91%EC%97%85%EC%9D%98%2080%25%EB%8A%94%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%A5%BC%20%EB%A7%8C%EC%A7%80%EB%8A%94%20%EA%B2%83%EC%9D%B4%EC%96%B4%EC%95%BC%20%ED%95%A8.%20%EC%8B%9C%EA%B0%81%ED%99%94%EB%8A%94%20%EB%B6%84%EC%84%9D%EC%9D%98%20%EC%B5%9C%EC%A2%85%EA%B2%B0%EA%B3%BC.%20d3%2Darray%20%EC%99%80%20d3%2Ddsv%EB%A5%BC%20%EA%B0%80%EC%9E%A5%20%EB%A7%8E%EC%9D%B4%20%EC%93%B0%EA%B3%A0%2C%20tidy.js%20%EB%82%98%20Arquero%20%EA%B0%99%EC%9D%80%20%EB%8F%84%EA%B5%AC%EA%B0%80%20%EB%82%98%EC%99%80%EC%84%9C%20%EA%B8%B0%EC%81%A8)이라고 했지만, 가시화 분야에 전문 지식을 갖춘 사람이 가시화를 만지는 시간이 전체 작업 시간의 80%를 차지하는 일도 가능해야 함.
			- 그러나 여전히 논란의 여지가 있음. 이것 매체의 투명도와 유사한 논의이기도 함. 만약 어떤 데이터를 쉽게 이해할 수 있다면 가시화 방법론이 매우 쉽고 직관적이어야 함. 익숙함 또한 이러한 특징에 기여할 수 있는데 바꿔서 얘기하면 가시화 전문가는 별난 시각적 효과를 창작하는 사람이어서는 안 됨. 오히려 반대로 가시화 전문가의 가장 기본적인 능력은 복잡한 데이터를 가장 전통적이고 단순한 가시화 도구, 대개는 도표(차트)에 사상(mapping)할 수 있는 능력을 갖춰야 함.
			- 반대로 가시화 전문가가 갖춰야 할 최고의 전문성은 데이터와 가시화 방법 사이에 괴리가 존재하는 가를 명확히 짚을 수 있어야 함. 만약 기존 가시화보다 더 투명성이 높은 다른 시각적 방법을 제안할 수 있다면 이 부분이야말로 가시화 전문가의 창의적 역량(creative expertise)으로 남을 수 있을 거임.
- ## log
	- [[2026-07-14]] Page created.
- ### References
	-