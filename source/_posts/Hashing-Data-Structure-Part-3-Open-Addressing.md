---
title: Hashing Data Structure | Part 3 (Open Addressing)
date: 2019-12-05 23:14:44
tags:
    - [Data Stracture]
    - [Hashing]
categories:
    - [Data Structure]
    - [Hashing]
---

### Open Addressing
Like separate chaining, open addressing is a method for handling collisions. In Open Addressing, all elements are stored in the hash table itself. So at any point, size of the table must be greater than or equal to the total number of keys(Note that we can increase table size by copying old data if needed).

<!-- more -->

> **Insert(k)**: Keep probing until an empty slot is found. Once an empty slot is found, insert k.
> **Search(k)**: Keep probing until slot's key doesn't become equal to k or an empty slot is reached. 
> **Delete(k)**: Delete operation is interesting. If we simply delete a key, then search may fail. So slots of deleted keys are marked specially as "deleted".

Insert can insert an item in a deleted slot, but the search doesn't stop at a deleted slot. 

### Open Addressing is done following ways
#### A. Linear Probing: 
In linear probing, we linearly probe for next slot. For example typical gap between two probes is 1 as taken in below example also. 
	
Let **hash(x)** be the slot index computed using hash function and S be the table size. 
	
If slot **hash(x) % S** is full, then we try **(hash(x) + 1) % S**
If slot **(hash(x) + 1) % S** is also full, then we try **(hash(x) + 2) % S**
......
......


Let's consider a simple  hash function as **"key mod 7"** and sequence of keys as 50, 700, 76, 85, 92, 73, 101

| index(0) |
|:--------:|
| index(1) |
| index(2) |
| index(3) |
| index(4) |
| index(5) |
| index(6) |


(Initial Empty Table)

|    &emsp;    |
|:------------:|
| 50(index(1)) |
|    &emsp;    |
|    &emsp;    |
|    &emsp;    |
|    &emsp;    |


(Insert **50**, (50%7 = _1_))

|   700  |
|:------:|
|   50   |
| &emsp; |
| &emsp; |
| &emsp; |
| &emsp; |
|   76   |


(Insert **700**, (700%7 = _0_) and **76**, (76%7 = _6_))
		
|   700  |
|:------:|
|   50   |
|   85   |
| &emsp; |
| &emsp; |
| &emsp; |
|   76   |


(Insert **85** (85%7 = _1_) : Collision Occurs, insert **85** at next free slot: 85%7 = _1_, (1+1)%7 = _2_)
		
|   700  |
|:------:|
|   50   |
|   85   |
|   92   |
| &emsp; |
| &emsp; |
|   76   |


(Insert **92**, (92%7 = _1_), Collision occurs as 50 is there at index _1_, insert at the next free slot : (1+1)%7 = _2_, 85 is there, next free slot: (2+1)%7 = _3_, insert **92** at index _3_)
		
|   700  |
|:------:|
|   50   |
|   85   |
|   92   |
|   73   |
|   101  |
|   76   |


(Insert **73**, (73%7 = 3), 92 at index _3_, next free slot: (3+1)%7 = 4, insert **73** at index _4_.)
(Insert **101**, (101%7 = 3), 92 at index _3_, next free slot: (3+1)%7 = 4, 73 at index _4_, next free slot: (4+1)%7 = 5, insert **101** at index _5_)
		
**Clustering** : The main problem with linear probing is clustering, many consecutive elements from groups and it starts taking time to find a free slot or to search an element. 

#### B. Quadratic Probing
We look for **i^2th** slot in **i'th** iteration.
	
Let **hash(x)** be the slot index computed using hash function.

If slot **hash(x) % S** is full, then we try **(hash(x) + 1*1) % S**
If **(hash(x) + 1*1) % S** is also full, then we try **(hash(x) + 2*2) % S**
If **(hash(x) + 2*2) % S** is also full, then we try **(hash(x) + 3*3) % S**
.....
.....

#### C. Double Hashing
We use another hash function **hash2(x)** and look for **i*hash2(x)** slot in **i'th** rotation.

Let **hash(x)** be the slot index computed using hash function.

If slot **hash(x) % S** is full, then we try **(hash(x) + 1* hash2(x)) % S**
If **(hash(x) + 1* hash2(x)) % S** is also full, then we try **(hash(x) + 2* hash2(x)) % S**
If **(hash(x) + 2* hash2(x)) % S** is also full, then we try **(hash(x) + 3* hash2(x)) % S**
.....
.....
	

### Comparison of above three
- Linear probing has the best cache performance but suffers from clustering. One more advantage of linear probing is **easy to compute**.
- Quadratic probing lies between the two in terms of cache performance and clustering. 
- Double hashing has poor cache performance but **no clustering**. Double hashing requires more computation time as two hash functions need to be computed. 


| &emsp; | Separate Chaining	 | Open Addressing |
|:------:|:---------------------:|:---------------:|
|   1    |	Chaining is Simpler to implement |	Open Addressing requires more computation |
|   2    |	In chaining, hash table never fills up, we can always add more elements to chain |	In open addressing, table may become full |
|   3    |	Chaining is less sensitive to the hash function or load factors |	Open addressing requires extra care for to avoid clustering and load factor. |
|   4    |	Chaining is mostly used when it is unknown how many and how frequently keys may be inserted or deleted |	Open addressing is used when the frequency and number of keys is known |
|   5    |	Cache performance of chaining is not good as keys are stored using linked list |	Open addressing provides better cache performance |
|   6    |	Wastage of Space(Some Parts of hash table in chaining are never used) |	In Open addressing, a slot can be used even if an input doesn't map to it |
|   7    |	Chaining uses extra space for links	 | No links in Open addressing |

#### Performance of Open Addressing
Like chaining, the performance of hashing can be evaluated under the assumption that each key is equally likely to be hashed to any slot of the table(simple uniform hashing)

**m** = Number of slots in the hash table
**n** = Number of slots to be inserted in the hash table

Load factor **α = n / m ( < 1)**

Expected time to **search/insert /delete < 1 / (1 - α)**

So Search, Insert and Delete take **(1 / (1 - α))** time
