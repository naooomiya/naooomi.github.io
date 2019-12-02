---
title: '[LeetCode] 760. Find Anagram Mappings'
date: 2019-11-30 23:28:04
tags:
    - [LeetCode(Easy)]
    - [Hashing]

categories:
    - [LeetCode Easy]
    - [Hashing]
---

### Description
Given two lists **A** and **B**, and **B** is an anagram of **A**. **B** is an anagram of **A** means **B** is made by randomizing the order of the elements in **A**.
We want to find an index mapping **P**, from **A** to **B**. 
**A** mapping **P[i] = j** means the ith element in **A** appears in **B** at index j.
These lists **A** and **B** may contain duplicates. If there are multiple answers, output any of them.

<!-- more -->

---

#### Example
For example, given

> A = [12, 28, 46, 32, 50]
> B = [50, 12, 32, 46, 28]

We should return
> [1, 4, 3, 2, 0]

as **P[0] = 1** because the 0th element of **A** appears at **B[1]**, and **P[1]** = **4** because the 1st element of A appears at **B[4]**, and so on.

#### Note:
**A**, **B** have equal lengths in range **[1, 100]**.
**A[i]**, **B[i]** are integers in range **[0, 10^5]**.

---

### Solution
**P[i] = j**, **A[i] = B[j]**. Traverse list **A**, map each value of **A** to its index in **B**. 
And before that, we need to traverse **B**, and find a hash table that can map value of **B** to its index

```java
class Solution {
    public int[] anagramMappings(int[] A, int[] B) {
        // key is the index value from B
        // value is the index from B
        Map<Integer, Integer> mapB = new HashMap();

        for (int i = 0; i < B.length; i++)
            mapB.put(B[i], i);

        int[] result = new int[A.length];
        for (int j = 0; j < A.length; j++)
            result[j] = mapB.get(A[j]);

        return result;
    }
}
```

### Time Complexity
Traverse list **A** and **B** : **O(n)**

### Space Complexity
Use a hash table to store the mapping from value of **B** to its index: **O(n)**