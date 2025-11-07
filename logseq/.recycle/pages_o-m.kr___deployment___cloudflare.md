date-created:: [[2025-10-30]]
date-modified::
division:: [[makr]]
stack:: [[frontend]]
tags:: [[deployment]], [[cloudflare]]
type::
status:: [[ai-generated]]

- ## Summary
	- Defines the deployment architecture for an Astro static site, utilizing Vercel for hosting and placing Cloudflare at the forefront to maximize security and global CDN performance.
	- Vercel is responsible for building and origin hosting, while Cloudflare handles domain management, DDoS defense, WAF, and edge caching.
	- The key configuration is ensuring the Proxy Status in Cloudflare is set to Proxied (Active).
- ## Steps
	- ### Pipeline
		- {{renderer :mermaid_6902f9ae-bea8-4cf7-91e0-fa0b07fdc29f, 3}}
		  collapsed:: true
			- ```mermaid
			  graph TD
			      A[conent request] --> B[Cloudflare DNS];
			      B --> C[Cloudflare CDN Cache]
			      C -->|Cache HIT| D[Resonse]
			      C -->|Cache MISS| E["Vercel CDN (Origin)"]
			      E -- [Origin renews the cache] --> C
			  ```
	- ### 1. Development and Integration (CI/CD Pipeline)
		- Commit and push the Astro source code to the GitHub Repository.
		- GitHub Actions detects PUSH/MERGE events and triggers the CI/CD pipeline.
		- Vercel executes the Astro static file build and hosts the static files on its own CDN.
	- ### 2. User Request and Delivery Flow
		- The user's domain request first enters Cloudflare's DNS and security layer.
		- If the content is in the Cloudflare CDN cache (`Cache HIT`), it responds immediately, providing the fastest response.
		- If the cache is missed or the TTL(Time To Live) is expired, the request is forwarded to the Vercel CDN (Origin Server).[^1]
		- Cloudflare receives the final content from Vercel, caches it, applies security, and delivers the final response to the user.
	- ### 3. Core Connection Settings (DNS Configuration)
		- A and CNAME records required by Vercel must be added to the Cloudflare DNS settings.
		- It is mandatory that the **Proxy Status** for all Vercel connection records is set to **Proxied (Active)**.
- ## Troubleshooting
	- **Cloudflare Double Caching Check:** Since both Cloudflare and Vercel use a CDN, check the cache settings (TTL) on both sides in case of caching issues, and adjust Cloudflare's caching rules as necessary.
	- **Proxy Status:** If the DNS record's Proxy Status is set to 'DNS only', the benefits of Cloudflare's security and CDN will not be applied, so Proxied status must be verified.
- ## log
	- [[2025-10-30]] Page created.
- ### References
	- [[astro_vercel_cloudflare_diagram_en.md]]
- ## Footnotes
	- [^1]: TTL referes to the duration for which cached content remains valid on server. For intance, if a cached contents has a TTL of 3600 seconds and tha titme has expired, Cloudflare CDN will forward the client's request to the origin server, retrieve the content, and cache it again.