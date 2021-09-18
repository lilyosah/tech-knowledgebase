# Testing
%%
#topic
#concept
**Related:**
-  

%%

==Verification:== making sure the thing works correctly
==Validation:== making sure you built the right thing 
==Coverage:== the % of code paths that are tested. There are different definitions of coverage and it's impossible by most standards to meet 100% of test coverage
- Does not imply that all code has really been tested, ex: short circuiting and expressions, may never evaluate the second half

## Types of tests
==Unit testing:== makes sure a single method does what it's supposed to
==Module testing:== tests across individual units
==Integration testing:== ensures that interfaces between units have consistent assumptions and communicate correctly
==Acceptance/system testing:== tests to see if the integrated program meets its specifications

## Testing practices
==Behavior-Driven Development (BDD):== building development around user stories, non-technical user cases etc.
- You can divide and conquer and write different tests at different points in development
==Test-driven development:== write tests first, for the code you want to have
- There's no actual evidence that writing tests before is better

==Regression testing:== automatically rerunning old tests so that changes don't break what used to work
==Continuous integration testing:== continuous regression testing vs. later phases