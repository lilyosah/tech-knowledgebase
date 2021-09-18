# Sets
#algo/data-structures 
#concept
**Related:**
-  [[Data Structures]]

---

## Definition 
[Interface Set\<E\>](https://docs.oracle.com/javase/7/docs/api/java/util/Set.html)

: unordered collection that contains no duplicate elements

- The textbook says bags only support insertion and iteration, not necessarily deletion
- Sets support deletion and other mathematical set functions like union and intersection

<br/>

## Implementations
### HashSet
[java.util.HashSet\<E\>](https://docs.oracle.com/javase/7/docs/api/java/util/HashSet.html)

> ✨ ALL operations are $O(1)$, iteration in $O(n)$
> 📝 Bad hash code functions can make a program unexpectedly run slower

#### Runtime

| Method       | HashSet               |
| ------------ | --------------------- |
| add(item)    | $O(1)$                |
| remove(item) | $O(1)$                |
| contains     | $O(1)$                |
| size         | $O(1)$                |
| iterator     | iterations are $O(n)$ |
