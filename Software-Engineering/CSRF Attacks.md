# Cross-site Request Forgery (CSRF) Attacks
#📥 
%%
#coding #SWE 
#concept

**Related:**
-  [[DevOps]]

%%

- Trick user's browser into visiting a different website for which user has a valid cookie; allows browser to act on behalf of the malicious entity using the user's privileges  
- Allows an attacker to modify application state on behalf of a user who is logged into an application

## Avoiding
(Strong) Include session "nonce" with every request  
In Rails:
- `csrf_meta_tags` in `layouts/application.html.haml`  
- `protect_from_forgery` in ApplicationController  
- These are automatically included in every Rails app  
- Rails form helpers automatically include nonce in forms  

(Paranoid) Prevent GET requests from having side-effects (like bank transfers)  
- Can restrict at the routing level, or within a controller