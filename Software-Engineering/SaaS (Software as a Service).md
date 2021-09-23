# Saas
#📥 
%%
#topic
#concept
%%
**Related:**
-  [[Cloud Computing]]


: Software as a service 

- New versions of apps can be piloted on a subset of customers before rolling out to all
- Data associated with the app is kept with the service
- A good fit when a group of users wants to collectively interact with the same data
- Often service-oriented architecture (SOA)
- Often uses [[Design Patterns#Client-Server]]


## Communication
- Uses HTTP routes

==Network Protocol:== Set of communication rules on which agents participating in a network agree 
==Transmission Control Protocol/Internet Protocol (TCP/IP):== Fundamental protocol linking all computers on the Internet 
- DNS has its own protocol based on TCP/IP that maps hostnames (www.lilydavisson.com) to IP addresses
- Establishing a TCP/IP connection requires a port number from 1 - 655435 to indicate which program on the server is the intended communication partner 

==HTTP Protocol:== Rules for communication to make a request and receive a response
1. Initiate TCP/IP connection by specifying ip and port number
2. If successful, sends a request to perform an operation on a resource (web page, image, form submission, etc.)
3. Server delivers a response

- Stateless, all requests are unrelated 

==Service Oriented Architecture:== A set of independent services composed to produce larger sites
==Microservice:== A standalone service that performs just one type of task