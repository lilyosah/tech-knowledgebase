# Networks
#📥 
%%
#concept
%%
**Related:**
-  [[SaaS (Software as a Service)]]

--- 

==Network Protocol:== Set of communication rules on which agents participating in a network agree 

## Transmission Control Protocol/Internet Protocol (TCP/IP
: Fundamental protocol linking all computers on the Internet 

- IP addresses identify a physical network interface with four octets 
- Establishing a TCP/IP connection requires a port number from 1 - 655435 to indicate which program on the server is the intended communication partner in additional to the IP
	- 443 is HTTPS (encrypted)
	- 80 is HTTP (not encrypted)
- IP is a "best effort service", but packets may be dropped, additional protocols (TCP) are layered on top to make more reliable
	- Detects and resends dropped, mangled, out-of-order packets, adapts to slow networks or hosts 

### DNS
- DNS has its own protocol based on TCP/IP that maps host names (www.lilydavisson.com) to IP addresses
- DNS has hierarchical structure 


## HTTP Protocol 
: Rules for communication to make a request and receive a response
- Text-based request/reply protocol for transferring web content
- Uses port 80 by default
- By default, stateless. All requests are unrelated, does not keep any history
	- The illusion of state is cookies

1. Initiate TCP/IP connection by specifying ip and port number
2. If successful, sends a request to perform an operation on a resource (web page, image, form submission, etc.)
3. Server delivers a response

### Cookies
- Key value
- Used to store info about requests
- Used for tracking
- [[Authentication]] (logged in or not)

### Requests
Include:
- Methods (GET, PUT, POST, DELETE...)
- ==Uniform Request Identifier (URI):== The path after the domain name to whatever query params there are 
- HTTP protocol version understood
- Headers: Extra info
	- Params use + instead of space
	- Params follow ? after URI, separated by &

### Responses
- Protocol version and status code 
	- 2xx, 3xx (resource moved), 4xx (client error), 5xx (server error)
- Response headers
- Response body

### Representational State Transfer (REST) 
: Conventions to indicate how URIs are constructed or how tasks should occur. Self-contained requests specify what resources to operate on and what to do with it
- 📝 Roy Fielding's PhD thesis
- Resource may be existing content or a request to modify something
- All state affecting the resource is explicit
- Common operations are ==CRUDI:== Create Read Update Delete Index, maps to operations
	- **Create** - POST
		- Ex: /books
	- **Read** - GET
		- Ex: /books/:id
	- **Update** - PUT or PATCH
		- Ex: /books/:id
	- **Delete** - DELETE
		- Ex: /books/:id
	- **Index** - GET: Get listing of ALL books
		- Ex: /books


## Other things:
- ==CNAMEs:== Aliases for other URI paths?  #🔍
- ==CURL:== Command line program used for making requests 
- ==Idempotent:== Can be retired with no side effects
	- GET requests
	- Non-idempotent: PUT, POST... (modifying requests)