date-created:: [[2025-08-05]]
date-modified::
division::
stack::
tags:: css, tailwindcss
type::
public:: true

- ## Summary
	- The fasted [[tailwindcss]] testing environment
- ## Steps
	- ### Requirements
		- [[vs code]] with [live server extension](https://github.com/ritwickdey/vscode-live-server).
	- ### Configurations
		- ```bash
		  npm install tailwindcss @tailwindcss/cli
		  ```
			- following [Tailwind CLI - Tailwind CSS](https://tailwindcss.com/docs/installation/tailwind-cli)
		- Set folder structure as below. **This is to test multiple layout with a single CSS file using `@import`**
			- ```bash
			  |   package-lock.json
			  |   package.json
			  |   tailwind.config.js
			  \---src
			      \---om
			          +---layouts
			          |   \---article
			          |           index.html <-- This file should import the css file, ../../styles/global.css 
			          \---styles
			                  global.css <-- CLI will automatically generate this file.
			                  input.css <-- file that you will edit.
			                  theme.css
			                  typography.css
			  ```
		- Edit `input.css` as below
			- ```css
			  /*  src\om\styles\input.css */
			  @import "tailwindcss";
			  ```
		- Change `tailwind.config.js`.
			- ```js
			  // tailwind.config.js
			  module.exports = {
			    content: ["./src/**/*.html"],
			    theme: {
			      extend: {},
			    },
			    plugins: [],
			  }
			  ```
			- This is to scan the html files then generate CSS output.
		- Now register `npm run dev` to run the tailwind CSS CLI command in `package.json` file
			- ```bash
			  // package.json
			  {
			    "dependencies": {
			      "@tailwindcss/cli": "^4.1.11",
			      "tailwindcss": "^4.1.11"
			    },
			    "scripts": {
			      "dev": "npx @tailwindcss/cli -i ./src/om/styles/input.css -o ./src/om/styles/global.css --watch"
			    }
			  }
			  ```
		- Check again your html file is loading the result file, `./src/om/styles/global.css` from above.
			- ```html
			  <!-- src\om\layouts\article\index.html -->
			  
			  <!DOCTYPE html>
			  <html lang="ko">
			    <head>
			      <meta charset="UTF-8" />
			      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
			      <title>o-m.kr</title>
			      <link rel="stylesheet" type="text/css" href="../../styles/global.css" />
			    </head>
			  ```
			- **Open this file with `Live Server` on [[vs code]]**. Then your default browser will open the location of your html file on localhost.
	- ### Result
		- As you edit `input.css`, the browser will udpate the result.
- ## Troubleshooting
	-
- ## log
	- [[2025-08-05]] Page created.
- ### References
	- [Tailwind CLI - Tailwind CSS](https://tailwindcss.com/docs/installation/tailwind-cli)
	-