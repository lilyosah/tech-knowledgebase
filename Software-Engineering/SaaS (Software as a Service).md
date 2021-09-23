# Saas
#📥 
%%
#topic
#concept
%%
**Related:**
-  [[Cloud Computing]]
-  [[Design Patterns]]
-  [[Networks]]


: Software as a service 

- New versions of apps can be piloted on a subset of customers before rolling out to all
- Data associated with the app is kept with the service
- A good fit when a group of users wants to collectively interact with the same data
- Often service-oriented architecture (SOA)
- Often uses [[Design Patterns#Client-Server]], sometime [[Design Patterns#Peer-to-peer Architecture]]
- Communicate using [[Networks]]


==Service Oriented Architecture (SOA):== A set of independent services composed to produce larger sites
- App divided into sub-parts with a clear external interface
- Sub-parts cannot access eachother's data without an interface (API)


==Microservice:== A standalone service that performs just one type of task
- Dividing service components into their smallest possible parts
- Pros: Each sub-component is independent and easy to evolve, components may be reused by multiple services 
- Cons: Performance is lower, complexity is higher


## APIs
Key issues that must be resolved:
1. How does caller (user) identify callee? (server)
	- HTTP endpoints
2. Which operation is called?
	- Operations on resources in a RESTFUL sense [[Networks#Represential State Transfer REST]]
	- URI and HTTP encodes the operation
	- CRUDI [[Networks#Represential State Transfer REST]]
3. How are args passed?
	- HTTP query params or HTTP payload
4. How does caller receive return value?
	- Response headers/HTTP response
5. How do we signal errors?
	- HTTP status codes