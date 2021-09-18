# DP and Greedy Interval Scheduling Example

---

Class: #algo/dynamic-programming 
Week: #week/week-9 
Tags: 
Related:
- [[Dynamic Programming]]
- [[Greedy Algorithms]]

---

## Description
You are given $n$ time intervals in a day. 

For each interval $i$, you are given
- its start time $s_i$
- its end time $f_i$
- its weight $w_i$

You want to pick the best set of intervals to schedule. This is a subset such that:
- they are non-overlapping (no interval's start time lies between another's start and finish times)
- the sum of their weights is maximized

**Ex: ✏**  
Input: 
1. $s_i$ = 2, $f_i$ = 6, $w_i$ = 2
2. $s_i$ = 5, $f_i$ = 10, $w_i$ = 5
3. $s_i$ = 9, $f_i$ = 13, $w_i$ = 6
4. $s_i$ = 12, $f_i$ = 14, $w_i$ = 4

Solution: The optimal schedule includes intervals 2 and 4. The sum of the weights is 9

<br/>

### What must be true for the solution?
- Either doesn't include interval 1, or does
	- If it **doesn't**, it should optimally include a subset of intervals 2 through $n$
	- If it **does**, it can't include any intervals that overlap with intervals 1 and optimally includes subset of what remains 

Remaining (intervals $k$ through $n$): Order the intervals by time, $k$ is the first interval with a start time $\ge$ than when interval 1 **finishes**
- So the ones that overlap are 1-$k$

<br/>

#### RT Analysis
Checking for overlapping intervals: $O(|S| \log_|S|$
- sort the intervals by start time
- for each interval, check if start time is earlier than the end time of the preceding interval

However, **all** possible schedules must be checked, and given $n$ intervals there are $2^n$ subsets of intervals (for every single interval there are two choices, scheduled or not)

<br/>

### A more simple version
**If all the intervals have equal weight**, then the max weighted version is just scheduling as many intervals as possible. 
Idea: Pick intervals so that we can leave as much time possible to schedule more intervals

#### Greedy Algorithm Idea
- sort by finish time
- for each interval, if start doesn't proceed finish time of one before, pick it

##### Justification
[[Greedy Algorithms#Exchange Argument]]
If there is another schedule chosen by another algorithm, in the first place where the schedules differ the other schedule must include an interval with a finish time no earlier than the one chosen by the greedy algorithm. If you swap that interval with one chosen by the greedy algorithm, you do no worse?

##### RT Analysis
- $O(n \log n)$ to sort
- $O(n)$ to iterate
- $O(n \log n)$ total 

<br/>

## General Version
The greedy doesn't work because it doesn't take the weight into account for our first example 

### Attempt 1: Brute Force Solution
Consider all possible schedules.
For each:
- check if there are overlapping intervals
- check the sum of weights of the schedules intervals

Keep track of the best set of non-overlapping intervals found, i.e, the sum of the weights. At the end, the highest sum wins.

<br/>

### Attempt 2: Recurrence Solution
Suppose intervals are ordered in terms of start time

Let $OPT(i)$ be the cumulative weight of the optimal schedule of intervals $i$ through $n$

$OPT(i)$ is the `max()` of:
- $OPT(i + 1)$ the case when we don't include $i$
or 
- $OPT(k)$, the case when we do include $i$, and $k$ is the earliest interval starting $\ge$ when $i$ finishes

$OPT(n) = W_n$: if there is one interval, then we should schedule it and the weight is its weight

```Python

def next_non_overlapping(intervals, i):
	# O(n) time per call, but can preproecss into a map for O(n^2) so all 
	# intervals, the reading assumes that this has been done so this 
	# costs O(1)
	k = i+1
	while k < n:
		if intervals[k].start > intervals[i].finish:
			break
		else:
			k += 1
	return k


def recurrence(intervals):
	# no intervals
	if len(intervals) == 0: 
		return 0
	# one interval remaining -> pick it
	if len(intervals) == 1:
		return {intervals[0]}, intervals[0].weight
	
	# if we don't choose the first interval, get everything else
	set1, weight1 = recurrence(intervals[1:])
	# get optimal version of everything else
	k = next_non_overlapping(intervals, 0)
	
	# If you do include the first, optimally schedule everything after 
	# the end of the first interval 
	set2, weight2 = recurrence(intervals[k:])
	
	# Compare the weights, pick the option that's better
	if weight1 > weight2 + intervals[0].weight:
		return set1, weight1
	else:
		set2.add(intervals[0])
		return set2, weight2 + intervals[0].weight


```

#### RT Analysis
Initial sort: $O(n \log n)$
Preprocessing the intervals to create a DP table for the next on-overlapping interval: $O(n^2)$
Recursive part: Make 2 recursive calls on at most $n - 1$ intervals.
- Recurrence: $T(n) = 2T(n - 1) + O(1)$
	- Two branches that do $n - 1$ is very bad 
	=> this evaluates to $O(2^n)$, same as brute force 
	
##### Redundant work being done
- We look at the same subset of intervals many times
	- You can get to the same "try $x$ through $n$" many times. (6 through $n$ for instance)
- You can avoid this by saving the work that you've already done, saving the $k$ through $n$ work you do in a structure [[Dynamic Programming#^634023]]
	- This means you only calculate $k$ through $n$ once for every $k$.

<br/>

### Attempt 3: Dynamic Programming version
You can eliminate the recursion because the answer for $OPT(k)$ will only be calculated when $OPT(K + 1)$ has already been done.
- Looking for smaller sub-problems, bottom-up approach

$OPT(k)$ depends on knowing the answers two two of the values $OPT(k')$ where $k' > k$ except when $k + n$ (because we know $OPT(n) = W_n$)
 
```Python
def cum_weights(intervals):
	#To calculate the cumulative weights
	OPT = new list[n+1]
	OPT[n] = 0
	OPT[n-1] = intervals[n-1].weight
	for k = n-1 to 0:
		x = next_non_overlapping(intervals, k)
		# try not picking interval k
		if OPT[k+1] > OPT[x] + intervals[k].weight:
			OPT[k] = OPT[k+1]
		# try picking interval k
		else:
			OPT[k] = OPT[x] + intervals[k].weight
	return OPT


def opt_sched(OPT):
	# given the weights, determine intervals
	intervals = new list
	i = 0
	while i < n:
		# optimal schedule for i, and remaining. If they're the same, 
		# skip i
		if OPT[i] == OPT[i+1]: # case 1: skip i
			i += 1
		# If not, should schedule i
		else: # case 2: include i
			intervals.add(i)
			i = next_non_overlapping(intervals, i)
	return intervals
```


#### RT with Memoization 
$O(n)$