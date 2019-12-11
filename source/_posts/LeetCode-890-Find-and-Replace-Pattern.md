---
title: '[LeetCode] 890. Find and Replace Pattern'
date: 2019-12-11 23:29:11
tags:
    - [LeetCode(Medium)]
    - [Hashing]
    - [String]

categories:
    - [LeetCode Medium]
    - [Hashing]
    - [String]
---
    
### Description:
You have a list of words and a pattern, and you want to know which words in words matches the pattern.
A word matches the pattern if there exists a permutation of letters p so that after replacing every letter x in the pattern with p(x), we get the desired word.
(Recall that a permutation of letters is a bijection from letters to letters: every letter maps to another letter, and no two letters map to the same letter.)
Return a list of the words in words that match the given pattern. 
You may return the answer in any order.

<!-- more -->

---

#### Example 1
    
> Input: words = ["abc","deq","mee","aqq","dkd","ccc"], pattern = "abb"
> Output: ["mee","aqq"]
    
#### Explanation 
"mee" matches the pattern because there is a permutation {a -> m, b -> e, ...}. 
"ccc" does not match the pattern because {a -> c, b -> c, ...} is not a permutation,
since a and b map to the same letter.
    
#### Note
1. 1 <= words.length <= 50
2. 1 <= pattern.length = words[i].length <= 20

---

### Solution

```java
class Solution {
    public List<String> findAndReplacePattern(String[] words, String pattern) {
        List<String> res = new LinkedList<>();
        for(String word : words)
        {
            if (checkPattern(word, pattern))
                res.add(word);
        }
        
        return res;
    }
    
    private boolean checkPattern(String word, String pattern)
    {
        if (pattern.length() != word.length()) return false;

        HashMap<Character, Character> map = new HashMap<>();

        for (int i = 0; i < word.length(); i++)
        {
            char w = word.charAt(i);
            char p = pattern.charAt(i);

            if (map.keySet().contains(w))
            {
                if (map.get(w) != p) return false;
            }
            else
            {
                if (map.values().contains(p)) return false;
                map.put(w, p);
            }
        }

        return true;
    }
}
```