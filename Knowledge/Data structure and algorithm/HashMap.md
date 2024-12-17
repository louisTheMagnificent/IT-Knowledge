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
Unlike chaining, open addressing does not use linked lists or other structures to store multiple elements that map to the same hash value. Instead, when a collision occurs, open addressing explores other locations in the hash table to find an empty slot to store the current element. When a new key needs to be inserted into the hash table and its calculated index position is already occupied, open addressing will follow some systematic probing sequence to find the next empty slot. This process continues until an empty slot is found or the table is confirmed to be full. We store key-value pairs in each bucket. There are three ways to fulfil open hashing:  
#### Linear probing  
New index = Original index + i (i is the number of search) 

If an index is already occupied, the probing process checks the next index in turn until an empty slot is found. This approach is simple to implement, but can lead to "clustering" problems, where multiple elements tend to cluster in a certain part of the table.
#### Quadratic probing  
New index = Original index + i^2 (i is the number of search)  

Quadratic probing is an improvement over linear probing in that, instead of simply checking the next index, the probing distance increases quadratically. This reduces clustering problems, but does not necessarily guarantee that an empty slot will be found, especially if the table is full.
#### Double hashing  
New index = (Original index + i(hash2(key))) mod m (i is the number of search. m is the size of the array. hash2() is 
a new hash function which returns a number which should be relatively prime with m to avoid infinite loop of searching)  

Double hashing effectively reduces collisions and improves the performance of hash tables by combining two independent hash functions, especially under high load factors. Choosing the right hash function is critical to ensuring the efficient operation of a hash table.
### Drawbacks of open addressing  
1. Deletion operations are more complex, because simply emptying a bucket may interrupt the search sequence. Usually deletions need to be handled by special markers (such as the DELETED state).
2. As the table approaches full, the performance of lookups and inserts can drop dramatically because more probes are required to find empty buckets or target keys.

## Rehashing  
Generally speaking, when the load factor of the hash table exceeds a certain threshold (such as 0.7 or 0.75), rehashing may be required. The new size of the hash table is typically twice the original size or a prime number close to twice that. Rehash each element in the old hash table and insert it into the new table. It should be noted that since the size of the hash table has changed, the original hash value is no longer applicable and the hash value of each element must be recalculated based on the new table size. Thus, rehashing consumes a lot of time. 
