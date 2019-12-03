---
title: '[LeetCode] 1160. Find Words That Can be Formed by Characters'
date: 2019-12-03 22:36:48
tags:
    - [LeetCode(Easy)]
    - [Hashing]

categories:
    - [LeetCode Easy]
    - [Hashing]
---

### Description
You are given an array of strings words and a string chars.
A string is good if it can be formed by characters from chars (each character can only be used once).
Return the sum of lengths of all good strings in words.

<!-- more -->

---

#### Example 1
Input: words = ["cat","bt","hat","tree"], chars = "atach"
Output: 6

> Explanation 
The strings that can be formed are "cat" and "hat" so the answer is 3 + 3 = 6.

#### Example 2
Input: words = ["hello","world","leetcode"], chars = "welldonehoneyr"

Output: 10

> Explanation
The strings that can be formed are "hello" and "world" so the answer is 5 + 5 = 10.

---

### Note
- 1 <= words.length <= 1000
- 1 <= words[i].length, chars.length <= 100
- All strings contain lowercase English letters only.

---

### Solution

```java
class Solution {
    public int countCharacters(String[] words, String chars) {
        int count = 0;
        Map<Character, Integer> map = new HashMap<Character, Integer>();
        for (char c : chars.toCharArray())
            map.put(c, map.getOrDefault(c, 0) + 1);
        
        // for each word
        for (String word : words)
        {
            Map<Character, Integer> wordMap = new HashMap<Character, Integer>();
            for (char c : word.toCharArray())
                wordMap.put(c, wordMap.getOrDefault(c, 0) + 1);
            
            boolean invalidWord = false;
            for (Character key : wordMap.keySet())
            {
                if (!map.containsKey(key) || map.get(key) < wordMap.get(key))
                    invalidWord = true;
            }
            if (!invalidWord)
            {
                count = count + word.length();
            }
        }
        return count;
    }
}
```