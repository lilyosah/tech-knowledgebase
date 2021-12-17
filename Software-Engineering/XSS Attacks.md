# Cross-Site Scripting (XXS) Attacks
#📥 
%%
#coding #SWE 
#concept

**Related:**
-  [[DevOps]]

%%

Attack works by injecting client-side executable code into the application pages  
- [[Javascript]] code added and re-rendered by a website can trigger execution of malicious scripts on other users' browsers.  
- E.g., JavaScript code that "leaks" cookies to a remote server  
- Can create leak by injecting image tag with URL of remote server but image 
"file" name with leaked information (i.e., leaked information appears directly in URL)

How do attackers inject malicious JavaScript code to carry out this attack?  
- Somehow get attack code to be saved to database of app  
- When page gets rendered to any user, malicious code gets rendered along with the app

## Avoiding
Sanitize any form inputs or any other data uploaded to your app  
- By default, [[Ruby Rails]] sanitizes all form inputs ("escapes" any HTML tags)  
	- All rendered text must be marked as safe in order for rendering to succeed  
- Sometimes you need to treat text as "raw", unescaped text in a view helper method  
- Use built-in method `html_safe` to mark a string as "safe", otherwise Rails will escape it
