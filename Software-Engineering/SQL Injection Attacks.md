# SQL Injection Attacks
#📥 
%%
#coding #SWE 
#concept

**Related:**
-  [[DevOps]]
-  [[SQL]]

%%

Using unsanitized form/parameter data directly in ActiveRecord (SQL) queries allows people to submit [[SQL]] calls that will actually be run. This can change data. 

## Avoiding
Sanitize your inputs! In [[Ruby Rails]]: use `?` params in `where` calls

