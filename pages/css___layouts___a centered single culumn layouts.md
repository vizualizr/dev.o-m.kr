date-created:: [[2025-07-30]]
date-modified::
division::
stack::
tags:: [[tailwindcss]] [[layout]] 
type::
public:: true

- ## Summary
	-
- ## Steps
	- ```html
	  <!DOCTYPE html>
	  <html>
	    <head>
	      <meta charset="UTF-8" />
	      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
	      <title>3.3 Binding data | D3.js in Action</title>
	      <link rel="stylesheet" type="text/css" href="./css/main.css" />
	    </head>
	    <body>
	      <main>
	        <div id="top">
	          <nav>GLOBAL NAV</nav>
	        </div>
	        <article>
	          <h2>3.3 Binding data | D3.js in Action</h2>
	  
	          <div class="svg-container"></div>
	  
	          <section></section>
	        </article>
	      </main>
	  
	      <div id="bottom">
	        <footer>
	          <div>FOOTER</div>
	        </footer>
	      </div>
	  
	      <!-- Load your scripts here -->
	      <script src="https://d3js.org/d3.v7.min.js"></script>
	      <script src="js/main.js"></script>
	    </body>
	  </html>
	  ```
	- ```CSS
	  @import "tailwindcss";
	  
	  body {
	      @apply bg-amber-50;
	      @apply flex flex-col min-h-screen items-center;
	  }
	  
	  main {
	      @apply w-full flex flex-col grow items-center;
	  }
	  
	  #top {
	      @apply flex flex-col h-12 items-center justify-center w-full bg-amber-100;
	  }
	  
	  nav {
	      @apply w-full max-w-3xl bg-blue-300;
	  }
	  
	  article {
	      @apply w-full max-w-3xl p-2;
	  }
	  
	  h2 {
	      @apply text-3xl my-2;
	  }
	  
	  .svg-container {
	      /* @apply max-w-3xl; */
	  }
	  
	  #bottom {
	      @apply flex flex-col h-24 items-center w-full p-2 bg-amber-100;
	  
	  }
	  
	  footer {
	      @apply bg-gray-400 max-w-2xl w-full;
	  }
	  ```
- ## Troubleshooting
	-
- ## log
	- [[2025-07-30]] Page created.
- ### References
	-