---
title: '[LeetCode] 383. Ransom Note'
date: 2019-12-10 23:51:40
tags:
    - [LeetCode(Easy)]
    - [Hashing]
    - [String]

categories:
    - [LeetCode Easy]
    - [Hashing]
    - [String]
---

### Description:
Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false. Each letter in the magazine string can only be used once in your ransom note.

<!-- more -->

---

#### Example
- canConstruct("a", "b") -> false
- canConstruct("aa", "ab") -> false
- canConstruct("aa", "aab") -> true

---

#### Note:
- You may assume that both strings contain only lowercase letters.

---

### Solution
#### One
##### Complexity Analysis : 
- Time Complexity: **O(Math.max(m,n))**
- Space Complexity: **O(1)**

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        if (ransomNote.length() > magazine.length()) return false;
        
        int len = ransomNote.length(), rPointer = 0, mPointer = 0;
        
        char[] rChars = ransomNote.toCharArray();
        Arrays.sort(rChars);
        char[] mChars = magazine.toCharArray();
        Arrays.sort(mChars);
        
        // Now the two character arrays are sorted, start to compare now
        while (len >= 0 && rPointer < rChars.length && mPointer < mChars.length)
        {
            if (rChars[rPointer] == mChars[mPointer])
            {
                len--;
                rPointer++;
                mPointer++;
            }
            else 
            {
                mPointer++;
            }
        }
        
        return (len == 0);
    }
}
```

#### Two
```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        Map<Character, Integer> map = new HashMap<>();
        
        for (int i = 0; i < magazine.length(); i++)
            map.put(magazine.charAt(i), map.getOrDefault(magazine.charAt(i), 0) + 1);
        
        for (int j = 0; j < ransomNote.length(); j++)
        {
            char c = ransomNote.charAt(j);
            if (map.containsKey(c))
            {
                map.put(c, map.get(c) - 1);
                if (map.get(c) < 0)
                    return false;
            }
            else
                return false;
        }
        
        return true;
    }
}
```