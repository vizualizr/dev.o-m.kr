date-created:: [[2025-08-01]]
date-modified::
division::
stack::
tags:: html
type::
public:: true

- ## Summary
	- Refer to the following list to structure an HTML document semantically, in accordance with web standards.
- ## Steps
	- ### `<hgroup>`
		- ```html
		  <hgroup>
		    <h1>Frankenstein</h1>
		    <p>Or: The Modern Prometheus</p>
		  </hgroup>
		  <p>
		    Victor Frankenstein, a Swiss scientist, has a great ambition: to create
		    intelligent life. But when his creature first stirs, he realizes he has made a
		    monster. A monster which, abandoned by his master and shunned by everyone who
		    sees it, follows Dr Frankenstein to the very ends of the earth.
		  </p>
		  ```
	- ### `<data>`
		- ```html
		  <p>New Products:</p>
		  <ul>
		    <li><data value="398">Mini Ketchup</data></li>
		    <li><data value="399">Jumbo Ketchup</data></li>
		    <li><data value="400">Mega Jumbo Ketchup</data></li>
		  </ul>
		  
		  // with <time> tag
		  <p>
		    The Cure will be celebrating their 40th anniversary on
		    <time datetime="2018-07-07">July 7</time> in London's Hyde Park.
		  </p>
		  
		  <p>
		    The concert starts at <time datetime="20:00">20:00</time> and you'll be able
		    to enjoy the band for at least <time datetime="PT2H30M">2h 30m</time>.
		  </p>
		  ```
- ## Troubleshooting
	-
- ## log
	- [[2025-08-01]] Page created.
- ### References
	- [HTML elements reference - HTML | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements#content_sectioning)