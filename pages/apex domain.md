date-created:: [[2025-07-25]]
date-modified::
division:: [[network]]
stack::
tags:: [[domain]] 
type::
public:: true

- ## Summary
	- what is apex domain
- ## Steps
	- What is apex domain?
	  logseq.order-list-type:: number
		- An Apex Domain, (Root Domain, Bare Domain, or Naked Domain), is the domain without any prefixes like "www" or other subdomains.
		  logseq.order-list-type:: number
		- Such as:
		  logseq.order-list-type:: number
			- google.com
			  logseq.order-list-type:: number
		- On the other hand, subsomains are:
		  logseq.order-list-type:: number
			- mail.google.com, calendar.google.com and so on.
			  logseq.order-list-type:: number
	- Cofigurations
	  logseq.order-list-type:: number
		- Apex domains
		  logseq.order-list-type:: number
			- To map an apex domain, from your domain service provider, you typically use an A record that points directly to the IP address of the web server. The reason is apex domains traditionally not allowed to use a CNAME record due to DNS specifications (a CNAME record cannot coexist with other records like NS or SOA on the same domain).
			  logseq.order-list-type:: number
		- Subdomains
		  logseq.order-list-type:: number
			- Most subdomains (like www.example.com, blog.example.com, dev.example.com, etc.) are typically mapped using a CNAME record when they point to another domain name.
			  logseq.order-list-type:: number
- ## log
	- [[2025-07-25]] Revised the AI answer.
- ### References
	-