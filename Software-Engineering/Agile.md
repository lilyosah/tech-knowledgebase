# Agile
%%
#coding 
#concept
**Related:**
-  [[Plan-document Models]]
-  

%%


Focuses mainly on improving existing code.
Practices center around successive refinement a working but incomplete software prototype until the customer is happy with the result. The customer offers feedback on each iteration, and each iteration is short.
Uses ==Behavior-Driven Design:== concentrates on the behavior of the app in conversation with the stakeholders before and during development.

## Manifesto
Do the important things more:
- Individual customer interactions
- Working software instead of documentation
- Customer collaboration
- Responding to change

Other features:
- [[Testing#Testing practices|Test driven development]]
- New versions every week or so, continuously improve a working prototype
- User stories instead of documentation

### Details
==Story points:== numbers indicating how long a story is expected to take. If it exceeds a certain agreed upon number it should be broken down into sub-stories
==Spikes:== a short investigation into a technique or problem that the team wants explored before sitting down to do serious coding 

#### User Stories
: 1-3 sentences written in non-tech language written jointly by customers and devs describing a use case/feature 

==Connextra format:==
- As a \[type of stakeholder]
- So that \[achieve some goal]
- I want to \[do some task]

==SMART stories:== 
- specific
- measurable (characterized with an acceptance test)
- achievable (w/in one iteration)
	- If you can't deliver it in one iteration, break it into smaller sub-tasks w/ fewer story points
- relevant ("5 whys")
- time-boxed (know when to give up)

#### UI Design
- ALL stakeholders should be involved in the UI
- Pen and paper designs first, "lo-fi" UI


## XP Variant 
Extreme programming
- Write [[Testing|tests]] before coding
This practice often employs 1-2 week iterations, behavior- and test-driven development and pair programming

## Testing
- Part of each iteration
- Each dev tests their own code
- Testing tools & processes are highly automated
- QA improves tools