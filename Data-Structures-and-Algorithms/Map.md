# Maps / Dictionaries
#algo/data-structures 
#concept
**Related:**
-  [[Data Structures]]

---

## Definition
[Interface Map\<K,V\>](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html)
: an unordered collection of (key, value) pairs that contains no duplicate keys (if you put two duplicates, the new will replace old)
- Also called symbol tables and maps

- Keys must be unique because they're how you identify items
- In an ordered **symbol table**, keys may be ordered
- **Maps** are iterable but unordered

 <br/>

## Implementations
### Unordered Implementation Strategies
1. List: keep keys in a list and a corresponding list can be used for values
	- finding a key and/or retrieving its value reduces to unordered list search
	- insertion and deleting must account for both keys and values
2. Hashing: convert elements to integers (.hashcode()) to integers and use those integers as indices in an array for fast lookup

### Ordered Implementation Strategies
1. List: same as above except keys are ordered
2. Tree: linked data structures that are ordered

### HashMap
[java.util.HashMap\<K,V\>](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html)

> ✨ All operations aside from iteration are $O(1)$
> 📝 Bad hash code functions can make a program unexpectedly run slower  

#### Runtime     

| Method           | HashMap               |
| ---------------- | --------------------- |
| get(key)         | $O(1)$                |
| put(key, value)  | $O(1)$                |
| containsKey(key) | $O(1)$                |
| remove(key)      | $O(1)$                |
| iterator         | iterations are $O(n)$ |