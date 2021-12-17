# Dev/Ops
#📥 
%%
#coding #SWE 
#concept

**Related:**
-  [[Development Basics]]

%%

Goal: To automate **everything.** You need rollbacks, etc. to be super easy. 

==Responsiveness:== how long do most users wait before the app delivers a useful response?
==Release Management:== how can you deploy or upgrade your app "in place" without reducing availability and responsiveness?
==Availability:== at percentage of the time is your app correctly serving requests?
==Scalability:== as the number of users increases, either gradually and permanently or as a one-time surge of popularity, can your app maintain its steady-state availability and responsiveness without increasing the operational cost per user?
==Privacy:== is important customer data accessible only to authorized parties, such as the data’s owner and perhaps the app’s administrators?
==Authentication:== can the app ensure that a given user is who they claim to be, by verifying a password or using third-party authentication such as Facebook Login or OpenID in such a way that an impostor cannot successfully impersonate another user without having obtained the user's credentials?
==Data Integrity:== can the app prevent customer data from being tampered with, or at least detect that tampering has occurred or that data may have been compromised?

## 3-Tiered Shared-Nothing Architecture
**Presentation tier:** web server which accepts HTTP requests from users and handles serving static assets. Forwards requests for dynamic content to the logic tier
**Logic tier:** where the actual app runs. Supported by an application server 
**Persistence tier:** store data that must persist across HTTP requests ([[Networks]])

HTTP's statelessness allows the presentation and logic tiers to be shared-nothing

Scaling presentation and application tiers: 
- Add virtual machines
- Reconfigure load balances

Scaling persistence tier: 
- Hard!
	- Sharding: Partition data scross multiple indepndent shards
		- Pros: Scales great if date is evenly divided
		- Cons: Bad if operations touch more than one table
	- Replication: replicate all data everywhere
		- Pros: Multi-table queries are fast 
		- Cons: Writes have to replicate every replica 

### Alternatives
Both of these are hard to do!
1. Use caching to reduce number of database accesses  
2. Avoid "`n+1` queries" problem in associations 
3. Use indexes judiciously

#### n+1 problem
When you are doing n+1 queries to traverse an association, rather than 1 query.

```Ruby
# Controller
# assumes class Customer with has_many :products, :through => :reviews.  
# in controller method:  
@buyers = Customer.where("zip = ?", code) # table scan if no index!  

# In the view  
<% @buyers.each do |buyer| %>  
	<% buyer.products.each do |product| %>  
		# BAD: each time thru this loop causes a new database query!
		<p><%= product.title %></p>
```

Solution: Eager loading 
In [[Ruby Rails]], with `.include`

```Ruby
# Controller
# Rails automatically traverses the through-association  
@buyers = Customer.where("zip = ?", code).includes(:products)  

# View
<% @buyers.each do |buyer| %>  
	<% buyer.products.each do |product| %>  
		# GOOD: this code no longer causes additional queries 
		<p><%= product.title %></p>
```

#### Indexes
Speeds up access when searching DB table by column other than primary key

Similar to using a hash table  
- The alternative is a linear table scan: bad!  
- Even bigger win if attribute is unique-valued

What to index:
- Foreign key columns
- Columns that appear in queries
- Columns on which you sort/filter 

Why not index every column?  
- Takes up space (i.e., there’s a space/time trade-off)

## Availability and Responsiveness
5 nines: 99.999% uptime
Hard for SaaS apps to get more than that: Upgrades gone bad, denial of service attacks, exceptions

### Responsiveness
SLO: Service-level objective 
Some quantitative goal for responsiveness
Apdex: Score between 0-1 that summarizes responsiveness according to a latency threshold parameter $T$

Response is:
- Satisfactory if completed within $T$
- Tolerable if completed within $4T$
- Unsatisfactory if > $4T$

$$
\text{Apdex} = (\text{satisfactory} + 0.5(\text{tolerable}))/N
$$

📝 Human threshold of perception is 100-200 milliseconds  
📝 Evidence suggests that response times above 8 seconds lead to users going elsewhere

### Upgrade Troubles
- During upgrade rollout, some instances will have the prev version, some the new
- If requires a destructive DB migration, you can't just drop the DB in production

> "A good rule of thumb for managing your production environment is to assume that any task you need to do in that environment will fail the first time and will have to be repeated from scratch."

Naive approach: 
1. Take service offline and apply destructive migration and copy data 
2. Deploy new code
3. Bring service back online

Feature flags:
1. Do non-destructive migration
2. Deploy method protected by feature flag
3. Flip flag on, if disaster, flip off
4. Once all records are moved, deploy the new code without the feature flag
5. Apply migration to remove old columns

Other uses for [[Feature Flags]] - In file

### Caching
Page caching: cache an entire page; request doesn't even hit Rails  
- Output of entire controller action is cached to disk  
- Requires some configuration in the webserver or caching front-end  
- Requires application to explicitly invalidate cached entries (“sweepers”)

Action caching: Like page caching, but can accommodate before actions on controller methods

Fragment caching (“Russian Doll caching”): arbitrary reusable parts of a page’s output are cached to avoid having to re-render them  
- Template rendering is one of the slowest aspects of a Rails app; fragment caching is designed to address this limitation  
- Termed “Russian Doll” caching because partials and nested partials can easily be cached
- Routing engine and dispatcher are still involved in requests  
- Generally no need to explicitly “expire” cached fragments  
- Engine creates a “cache key” based on what is being cached  
	- When content changes, cached entry will be expired/replaced automatically (but there are corner-cases where this won’t happen)  
	- This is called generational caching

[[Ruby Rails#Caching]]

## Attacks
### Break into server(s) hosting the application, steal confidential information  
- Store passwords in encrypted form  
- Don’t let confidential information leak into application logs (log masking)

### Launch man-in-the-middle attacks to hijack application and/or users  
- Use encryption (Transport Layer Security)  
- Protect against cross-site request forgery ([[CSRF Attacks]]/XSRF)

### Attempt to corrupt the application or force the app to expose private data  
- Mass assignment protection (strong parameters)  
	- Malicious entity could put extra info in POST calls, in Rails: `permit` and `require` in [[Rails Controllers]]
- Protect against [[SQL Injection Attacks]]  
- Protect against cross-site scripting ([[XSS Attacks]])  
- Escape and sanitize any form data

### Harvest information accidentally left in a public code repo  
- Make sure there is no secret information (e.g., passwords, keys) in Github!
	- API keys for 3rd party services  
	- App keys for 3rd party authentication  
	- Passwords of any kind
	- Solution: Use environment variables that can be set in the shell
		- Can configure these in Heroku too

### Launch denial of service attacks against a public-facing web server (or network service)
- Basic idea: hire a botnet or use some other mechanism to direct lots of garbage traﬀic toward a server  
- The cost is pretty low to launch mid-scale DoS attacks  
- There's nothing in the application itself that you can do  
- Best to use a service such as cloudflare to mitigate the damage  
- Network service providers may be able to help, to "blackhole" DoS traffic on upstream links

### Storing private info
Don't store any private info you don't have to (especially credit card info), if hosting provider is compromised it could all be stolen. If you **must** then encrypt it all at the very least  

Add parameters to your engine to hide them from your logs. In Rails, add parameters to: `config/initializers/filter_parameter_logging.rb`
Default setting: `Rails.application.config.filter_parameters += [:password]`