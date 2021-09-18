# Queues
#algo/data-structures 
#concept
**Related:**
-  [[Data Structures]]

---

## Definition
[Interface java.util.Queue\<E\>](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html)

: bag which supports remove in a first-in, first-out order (FIFO)

**Applications:**
- Preserving relative order during data processing
- Waiting lists
- Scheduling
- Expression eval.
- Breadth-first graph searching

## Implementations
### Linked List
- Often implemented by **linked-lists**

### Runtime

> ✨ RT for every implementation should be $O(1)$


| Method | Queue  |
| ------ | ------ |
| offer  | $O(1)$ |
| remove | $O(1)$ |