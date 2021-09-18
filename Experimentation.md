# Experimentation
#topic
#concept
**Related:**
-  [[IXP]]

---

Validating a change you're making to make sure you're making good changes or de-risk potential changes. Used frequently in marketing and communication. 

Once you figure out a customer problem, get a correct sample size to test a change, figure out what you're changing, the metrics you will measure along, etc., and then run your tests and work with analysts to determine if the change was useful. 

**Requires a good hypothesis:**
"If we change X to do X, we would see Y, and success would be a specific metric."

**Made up of:**
- Experiences: The changes you are making
- Experiment infrastructure: Getting experiments to customers 
	- ⭐[[IXP]] 
- Data: The results and analysis, getting the right data and analysis is important

==Experimentation culture:== A way of running a business, how do they go about their day-to-day, a way of making almost all decision

<br/>

## Definitions
==Treatment/Variant/Recipe/Bucket:== The change in one or more variables that is expected to impact user experience
==Control:== The baseline experience you want to measure against
==Assignment ID:== Identifies one entity in a group such as a company, visitors, mobile devices. Treatments can be applied to these entities
- 
==Traffic:== Percentage of eligible users that will be dedicated to a certain treatment
- ==Sample:== Sub-group of users that hopefully represent the entire group being experimented with
- ==Spectrum:== Array representation of site traffic where each array cell is a subdivision of entire site traffic 
- ==Cell:== Subdivision of site traffic
- ==Cell allocation:== Specifies which cells are allocated to a treatment. Assigned by assignment ID based hashing and cells allocated to a treatment 

## Types of experiments
*Downloaded an experiment test type matrix to desktop*
### Rapid Experimentation
Quick experiments used to discover new ideas
- Rapid prototyping
- Can experiment quickly as you build towards larger experiments
- Less risky

**When to use:** When you need to run smaller experiments that can be performed in 48 hours or less

### Targeting
Unique experience to a specific audience using ML
- Can be used to make more relevant experiences
- More risk

**When to use:** When there is evidence that members of a group will act differently when treated differently

### Usability
Testing by real users
- Shows if users are able to complete certain tasks and how long it takes
- Less risky

**When to use:** When a feature is being launched without experimentation or when you want to test a low-traffic area of the site

### Personalization
Like targeting but targets individuals on a 1:1 level instead of an audience, uses ML
- Highly targeted content is delivered based on the behavior of previous visitors with shared traits
- More risk

**When to use:** When you have a personalization engine and enough data and changes to deliver a personalized experience

### Multivariate Testing
Tests multiple elements, each with multiple variations
- Helps to show which elements effects metrics most and 
- The interaction effects between multiple elements
- More risk

**When to use:** On high traffic pages when you are considering multiple changes

### A/B/n
Tests two or more variations of one element
- Used to quickly evaluate preferences
- More treatments is better
- More risk

**When to use:** When you need to figure out which version with only one element being changed performs best

### Back Testing
Evaluating a change that was made without testing
- Real-time comparison of a new experience vs previous default experience

**When to use:** When a new experience is launched without testing but you still need to measure impact, also helpful to validate best performers in things like seasonal changes

### Feature Ramping
Measures the impact of planned changes
- Reduces risk of unforeseen impacts and allows for gradual rollout of a feature

**When to use:** As part of the dev cycle when a new feature is introduced ("feature flagging")