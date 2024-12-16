# HashMap
---
## Construction  
Hashmap is used to store key-value pairs to provide fast data insertion, search, and deletion operations. First we set a 
hash function to map the key to an integer value in a fixed range, called a hash code. Then we convert the hash code into 
a valid array index (using Remainder Operation and each position in the array is called bucket). Thus we can access the value based on the key directly.

---
## Hash collision  
But sometimes different key could be mapped into the same index which is called hash collision. We have two ways to deal with it.

### Chaining  
We do not store the value in the bucket directly. We store a pointer which points to a linked list, all the keys of values which
are mapped to the same index will be stored into the linked list. When a hash collision happens, the new value is added at the end of the linked list.
But in the worst case, the time complexity could be O(N), so in order to solve this, we use a binary balanced tree to store the values which decreases 
the time complexity to O(log(N)).  

### Open addressing
