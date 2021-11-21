# Testing
%%
#topic
#concept
**Related:**
-  [[Behavior Driven Design]]
-  [[Ruby#Testing]]

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

### Continuous Integration
- As changes happen to different code branches in a repo, run a battery of automated tests

### Classifications of tests
- There are multiple levels of coverage that can be obtained (C0 most common, statement coverage. Is every statement of the code executed once by the test suite?)

**S0:** Every method called
**S1:** Every method from every call site
**C0:** Every statement
**C1:** Every branch in both directions
	- Both parts of if/else
**C1+decision:** Every sub-expression in conditional
**C2:** Every path (difficult, and disagreement on how useful)

### Other
==Mutation testing:== deliberately changing code at runtime to make sure that it will fail
==Fuzz testing:== Throw random input at the code, tests apps the way it wasn't meant to be used
	- 🌎 Microsoft found that this found 20% of crash bugs
==DU-coverage:== is every pair (`define x/use x`) executed?
==Black box vs. white box:== About the kind of assumptions you make during testing
- Being oblivious of the internals or be aware and try to exploit/break it 


## Testing practices
Tests should be "FIRST:"
- **Fast:** Should be easy and fast to run the tests
- **Independent:** No test relies on other tests so that you can run only a subset of tests that cover recent changes/in any order
- **Repeatable:** Should not rely on external factors like the date or magic constants that will break the test if their values change 
- **Self-checking:** Tests should not need human checking to know if they passed
- **Timely:** Should be updated at the same time as the code they are for

==Behavior-Driven Development (BDD):== building development around user stories, non-technical user cases etc.
- You can divide and conquer and write different tests at different points in development

==Regression testing:== automatically rerunning old tests so that changes don't break what used to work
==Continuous integration testing:== continuous regression testing vs. later phases

### Mocking and Stubbing
==Stub:== A "fake" method that returns a pre-configured value
==Double:== fake object that stands in for some other object in the context of a test
- If you create a double object you'd need to stub every method you want it to have because double objects have no methods


### How much testing is enough?
(lines of code)/(lines of test)
code-to-test ratio 1.2-1.5 is not unreasonable
Better: "How thorough is my testing?"

## Structure of a Test Case
==System under test (SUT):== The object being tested. (Single method, group of methods, etc). Defined from the POV of the test
==Test case:== Check that some behavior does or does not happen for some SUT
==Test suite:== A collection of tests
==Left method:== A method that does not call any other methods
==Pure function:== Has no side effects, return val is always the same for the same arguments. The easiest type of function to test

Steps that must be followed to set up a test:
1. **Arrange** create any necessary preconditions for the test case (setting values of variables that affect the behavior or the SUT, etc.)
2. **Act** exercise the SUT
3. **Assert** verify that the result or behavior matches what was expected

- Choose assertions that each cover one code paths
- When arrangement is complicated/ there is nondeterminism, you can create method stubs or mock objects to return fixed desired values for a method/object instead of dealing with the actual one
- If a function has side effects, in arrange observe the relevant state, in assert observe again and check for side effects

### Test-Driven Development (TDD)
: write tests first, for the code you want to have
📝 There's no actual evidence that writing tests before is better
==Red-Green-Refactor:== The basic TDD workflow:
1. Write a test for one aspect of the behavior you want your code to have (CYWYH)
2. **Red:** Run the test to verify it fails
3. **Green:** Write the most simple code that causes this test to pass without breaking existing tests
4. **Refactor:** Look for opportunities to refactor your code or your tests 

