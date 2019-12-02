---
title: '[LeetCode] 961. N-Repeated Element in Size 2N Array'
date: 2019-12-01 22:54:02
tags:
    - [LeetCode(Easy)]
    - [Hashing]

categories:
    - [LeetCode Easy]
    - [Hashing]
---

### Description
In a array A of size **2N**, there are **N+1** unique elements, and exactly one of these elements is repeated **N** times.

Return the element repeated **N** times.

<!-- more -->

---

#### Example 1
Input: [1,2,3,3]
Output: 3

#### Example 2
Input: [2,1,2,5,3,2]
Output: 2

#### Example 3
Input: [5,1,5,2,5,3,5,4]
Output: 5

#### Note
1. 4 <= **A.length** <= 10000
2. 0 <= **A[i]** < 10000
3. **A.length** is even

---

### Solution

```java
class Solution {
    public int repeatedNTimes(int[] A) {
        Map<Integer, Integer> count = new HashMap();
        
        for (int x : A)
        {
            count.put(x, count.getOrDefault(x, 0) + 1);
        }
        
        for (int i : count.keySet())
        {
            if (count.get(i) > 1)
                return i;
        }
        throw null;
    }
}

```

### Time Complexity
**O(N)**, where N is the length of A

### Space Complexity
Space Complexity: **O(N)**