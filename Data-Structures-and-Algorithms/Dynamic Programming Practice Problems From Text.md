[Problem PDF](file:///C:/Users/Lily/Downloads/KT-DP6-Problems.pdf)
Password: 967RNW

# 10
## a)
*Switch if next cell of the other option is greater than the current and next cell of the current option*

|        | Min 1 | Min 2 | Min 3 | Min 4 | Min 5 |
| ------ | ----- | ----- | ----- | ----- | ----- |
| A      | ==1== | 0     | ==0== | 3     | 0     |
| B      | 0     | ==0== | 2     | ==0== | ==4== |
| Change | +1    | M, +0 | M, +0 | M, +0 | +4      |

1. Choose A
2. 0 + 0 < 2 so -> B 
3. 2 +0 < 3 so -> A 
4. 3 + 0 < 4 so -> B
5. Stay

Answer: 5
Correct: 7

*You can make it repeatedly switch back and forth when it shouldn't*

## b)
Give an efficient algorithm that takes values for $a_1,a_2, ... ,a_n$ and $b_1, b_2, ... ,b_n$ and returns the value of an optimal plan.


- At each step, you either add the thing you're currently on or you switch.

```
OPT(i, onTrackA):
	if i == n:
		return nth value of whatever track we are on
	value += Max(OPT(i, onTrackA)+ ith value on this track, OPT(i + 1, !onTrackA))
	// store these values using memoization
```

RT: $i$ work, (memoization) so $O(n)$

Iteratively:

```
for i:
	if i == n:
		value += nth value on this track
		return
	if 


```



