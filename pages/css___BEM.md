date-created:: [[2025-07-31]]
date-modified:: [[2025-08-05]] 
division:: [[frontend]] 
stack::
tags:: css
type::
public:: true
status:: [[ai-proofed]]

- ## Summary
	- ```css
	  .block__element--modifier {
	    // your style
	  }
	  ```
	- A rule to oranize your CSS code in effective manner for your colleagues
		- > This becomes especially important when you’re working with teams of themers, and when high performance is essential.
		  > [BEM -- Introduction](https://getbem.com/introduction/)
	- A glance of CSS should imply the structure of style in html page.
- ## Steps
	- ### Naming rule
		- #### units
		  logseq.order-list-type:: number
			- block
			  logseq.order-list-type:: number
				- A ==self-contained==  and reusable unit in the layout which has a specific ==role==.
				  logseq.order-list-type:: number
			- element
			  logseq.order-list-type:: number
				- A unit that is not able to work alone.
				  logseq.order-list-type:: number
			- Modifier
			  logseq.order-list-type:: number
				- any ==state==, thus a changes in any style or certain kinds, of given block or element.
				  logseq.order-list-type:: number
		- #### conventions
			- ##### `-` is not a structure seperato
				- Single dash, `-` is reserved soley for word connection.
				- Use double dash (`--`) for connecting an element, double underscore (`__`) for connecting a modifier. This helps avoid confusion.
			- ##### Chaning is incorrect
				- ```html
				  <!-- ANTI-PATTERN: Do NOT do this -->
				  <div class="card">
				    <div class="card__header">
				      <h2 class="card__header__title">My Card</h2>
				    </div>
				  </div>
				  ```
				- Becasue in BEM,  elements should not own other elements. If any element belongs to another it is not an element. It is a block.
				- ```html
				  <!-- CORRECT BEM STRUCTURE -->
				  <div class="card">
				    <div class="card__header">
				      <h2 class="card__title">My Card</h2>
				    </div>
				  </div>
				  ```
			- ##### Style with class, not the name of the tag.
				- ```html
				  <main>
				                <div class="header__info">
				                <ul  class="header__revisions">
				                  <li>작성일: <time datetime="2025-08-01">2025년 8월 1일</time></li>
				                  <li>갱신일: <time datetime="2025-08-02">2025년 8월 2일</time></li>
				                  <li>작성자: <a href="#" rel="author">진경수</a></li>
				                </ul>
				              </div>
				  </main>
				  ```
				- Let's say the `<main>` tag appears only once on this page, but BEM recommends styling it using a class name. Why?
					- The goal is **consistency**. Requiring both tag and class inspection to understand styling undermines consistency in the structure.
					- HTML tags are implicit, while CSS classes and IDs are **explicit**.
					- From a maintenance perspective, if the `<main>` element changes at the tag level, you’ll need to clear existing styles tied to `<main>`. But if your `<main>` styling is attached to a class, you can simply apply a different class to the tag on any new page.
	- ### Example
		- ```css
		  .block__elementA {
		    
		  }
		  
		  .block__elementA--dark {
		    
		  }
		  ```
		- ```html
		  <form class="form form--theme-xmas form--simple">
		    <input class="form__input" type="text" />
		    <input
		      class="form__submit form__submit--disabled"
		      type="submit" />
		  </form>
		  ```
		- ```css
		  .form { }
		  .form--theme-xmas { }
		  .form--simple { }
		  .form__input { }
		  .form__submit { }
		  .form__submit--disabled { }
		  ```
	- ### Strategy
		- #+BEGIN_IMPORTANT
		  Sometimes it may subjective to tell what is block and what is element.
		  #+END_IMPORTANT
		- Following the role-based approach.
- ## Troubleshooting
	-
- ## log
	- [[2025-07-31]] Page created.
	- [[2025-08-01]] Paraphrased the naming rules and the strategy.
	- [[2025-08-05]] Added rules and summary.
- ### References
	- [BEM naming rules, recommended.](https://getbem.com/naming/)