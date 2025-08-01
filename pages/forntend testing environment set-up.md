date-created:: [[2025-07-22]] 
date-modified:: [[2025-07-25]] 
stack:: [[forntend]] 
tags:: tailwindcss, vite, d3.js
type::
public:: true

- ## Summary
	- Build a Windows-based prototype environment for [[tailwindcss]] v4 with [[vite]] and [[d3.js]]
	- Establish a lightweight configuration with clear structure for iterative UI testing.
- ## Procedure
	- ### Project Initialization
		- ```Bash
		  npx create-vite@latest fastlab --template vanilla
		  cd fastlab
		  npm install
		  ```
	- ### Check Node.js Engine Compatibility
		- Vite 7.0.5 requires:
			- ```
			  Node.js ^20.19.0 || >=22.12.0
			  ```
		- The current version `v22.11.0` led to warning.
		- Upgraded to `v22.12.0` using `nvm` or manual installation.
	- ### Installation TailwindCSS v4
		- Installation and Setup to the project folder, `fastlab`
			- ```
			  npm install -D tailwindcss postcss autoprefixer
			  ```
			- Note that as of v4, `npx tailwindcss init -p` is no longer supported. Configuration is embedded via CSS and PostCSS.
		- Style File
			- ```
			  /* src/styles/style.css */
			  @import "tailwindcss";
			  ```
		- #### Configuring PostCSS ( `postcss.config.cjs` )
			- > Required in CommonJS format due to ES Module boundary:
			- ```js
			  module.exports = {
			  plugins: {
			    '@tailwindcss/postcss': {},
			    autoprefixer: {},
			  },
			  };
			  ```
			- >  `@tailwindcss/postcss` is the dedicated PostCSS plugin introduced in Tailwind v4.
	- ### Vite Configuration
		- ```js
		  // vite.config.js
		  import { defineConfig } from "vite";
		  
		  export default defineConfig({
		  css: {
		    postcss: "./postcss.config.cjs",
		  },
		  });
		  ```
	- TODO D3.js Installation and Test Integration
		- ```
		  npm install d3
		  ```
	- LATER Directory Listing Feature (Implementation Deferred)
		- Attempted integration using `sirv` middleware + `vite.config.js` + `server.mjs`.
		- Issues encountered:
			- `createServer()` does not auto-import `vite.config.js`.
			- `vite.middlewares.listen()` does not handle direct HTTP requests.
			- Even when wrapped with `http.createServer(vite.middlewares)`, directory listing did not render at root level.
	- Conclusion: Feature deferred. May require static file server (e.g. `http-server`, `serve`) or custom plugin.
- ## Directory Structure Overview
	- ```bash
	  fastlab/
	  ├── server.mjs
	  ├── vite.config.js
	  ├── postcss.config.cjs
	  ├── package.json
	  ├── index.html
	  ├── src/
	  │   ├── styles/
	  │   │   └── style.css
	  │   └── pages/
	  │       ├── bar-chart.html
	  │       └── bar-chart.js
	  ```
	- #### considerations
		- the below has tested but not fully compatible with my needs.
			- [GitHub - wesbos/vite-plugin-list-directory-contents: A Vite plugin to list folders contents when in dev mode](https://github.com/wesbos/vite-plugin-list-directory-contents) for directory listing with [[vite]]
			- [tiddlywiki](https://tiddlywiki.com/static/Formatting%2520in%2520WikiText.html) also was considered but leanring curve is too steep especially its formatting.
- ## Troubleshooting
	- [[2025-07-25]] [[vite]] prompts ENOENT error pop-up
		- Symptom
			- [[vite]] pops up the error with the message below.
				- > ENOENT: no such file or directory, scandir 'D:\yonggeun\www\fastlab\.well-known\appspecific\com.chrome.devtools.json'
			- This means some file is missing in the proejct folder.
		- Solution
			- Install [GitHub - ChromeDevTools/vite-plugin-devtools-json: Vite plugin for generating `com.chrome.devtools.json` on the fly in the devserver.](https://github.com/ChromeDevTools/vite-plugin-devtools-json)
				- ```bash
				  PS fastlab> npm list
				  fastlab@0.0.0 \fastlab
				  ├── @tailwindcss/postcss@4.1.11
				  ├── autoprefixer@10.4.21
				  ├── postcss@8.5.6
				  ├── sirv@3.0.1
				  ├── tailwindcss@4.1.11
				  ├── vite-plugin-list-directory-contents@1.4.5
				  └── vite@7.0.5
				  
				  # install the library
				  PS fastlab> npm install -D vite-plugin-devtools-json
				  
				  added 111 packages, changed 2 packages, and audited 278 packages in 5s
				  
				  36 packages are looking for funding
				    run `npm fund` for details
				  
				  4 moderate severity vulnerabilities
				  
				  To address all issues (including breaking changes), run:
				    npm audit fix --force
				  
				  Run `npm audit` for details.
				  
				  PS fastlab> npm list
				  fastlab@0.0.0 \fastlab
				  ├── @tailwindcss/postcss@4.1.11
				  ├── autoprefixer@10.4.21
				  ├── postcss@8.5.6
				  ├── sirv@3.0.1
				  ├── tailwindcss@4.1.11
				  ├── vite-plugin-devtools-json@0.3.0
				  ├── vite-plugin-list-directory-contents@1.4.5
				  └── vite@7.0.5
				  ```
- ### log
	- [[2025-07-22]] Tailwindcss and the vite configuration finished.