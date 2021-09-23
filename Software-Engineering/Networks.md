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
	- 443 is HTTPS
	- 80 is HTTP
- IP is a "best effort service", but packets may be dropped, additional protocols (TCP) are layered on top to make more reliable
	- Detects and resends dropped, mangled, out-of-order packets, adapts to slow networks or hosts 

### DNS
- DNS has its own protocol based on TCP/IP that maps host names (www.lilydavisson.com) to IP addresses
- DNS has hierarchical structure 


## HTTP Protocol 
: Rules for communication to make a request and receive a response
- Text-based request/reply protocol for transferring web content
- Uses port 80 by default
- Stateless, all requests are unrelated

1. Initiate TCP/IP connection by specifying ip and port number
2. If successful, sends a request to perform an operation on a resource (web page, image, form submission, etc.)
3. Server delivers a response

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
	- 2xx, 3xx (resource moved), 4xx (access problem), 5xx (server error)
- Response headers
- Response body

### Represential State Transfer (REST) 
: Conventions to indicate how URIs are constructed or how tasks should occur
- PUT and POST calls send the request in the body


## Other things:
- ==CNAMEs:== Aliases for other URI paths?  #🔍
- ==CURL:== Command li used for making requests 