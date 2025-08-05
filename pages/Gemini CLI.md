date-created:: [[2025-08-01]]
date-modified::
division:: 
stack::
tags::
type::
public:: true

- ## Introduction
	- A command line tool to send query to Google Gemini.
	- Agent mode has the privilege to creat, modify, and delete the files on the host.
- ## Steps
	- ### Installation
		- ```bash
		  # on windows and POSOX
		  npm install -g @google/gemini-cli
		  ```
		- As `-g` option attached, npm will add the library to the location where it manages packages at th global level.
		- So you can run this command any location of your system.
		- then, run it
			- ```bash
			  gemini
			  ```
		- for `brew` command, visit the Gemini-cli github repo from the below.
	- ### Configuration
		- #### authentication
			- via web prompt. Use your existing Google account. (limited to 60 model requests per minute and 1,000 model requests per day)
			- Get more details on [authentication page](https://github.com/google-gemini/gemini-cli/blob/main/docs/cli/authentication.md).
		- #### Gemini API Key
			- This key is equivalent with a free tier with 100 requests per day using **Gemini 2.5 Pro**.
			- Get your key from [Google AI Studio](https://aistudio.google.com/).
			- Via terminal add this key to your system as an `environmental variable`
			- ```bash
			  #POSIX
			  export GEMINI_API_KEY="The-key-you-received"
			  ```
			- ```powershell
			  # windows
			  # with Administrative privilege
			  
			  C:\Windows\System32>setx GEMINI_API_KEY "The-key-you-received"
			  SUCCESS: Specified value was saved.
			  ```
	- ### Application
		- #### run
			- ```bash
			  cd new-project/
			  gemini
			  > Write me a Gemini Discord bot that answers questions using a FAQ.md file I will provide
			  ```
		- or from github
			- ```bash
			  git clone https://github.com/google-gemini/gemini-cli
			  cd gemini-cli
			  gemini
			  > Give me a summary of all of the changes that went in yesterday
			  ```
- ## Troubleshooting
	-
- ### log
	- [[2025-08-01]] Installed.
		- the same page exists on the private logseq as a software item.
	- [[2025-08-01]] Failed to integrate the extension, [Gemini Code Assist](https://marketplace.visualstudio.com/items?itemName=Google.geminicodeassist) on [[vs code]] and Gemini-cli
		- [Gemini Code Assist Documentation](https://developers.google.com/gemini-code-assist/docs/overview)
- #### References
	- [[@google-gemini/gemini-cli]]