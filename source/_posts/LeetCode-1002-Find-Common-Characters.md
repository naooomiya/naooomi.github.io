---
title: '[LeetCode] 1002. Find Common Characters'
date: 2019-12-09 23:56:10
tags:
    - [LeetCode(Easy)]
    - [Hashing]

categories:
    - [LeetCode Easy]
    - [Hashing]
---

### Description
Given an array A of strings made only from lowercase letters, return a list of all characters that show up in all strings within the list (**including duplicates**).  
For example, if a character occurs 3 times in all strings but not 4 times, you need to include that character three times in the final answer.
You may return the answer in any order.

<!-- more -->

---

#### Example 1
Input: ["bella","label","roller"]
Output: ["e","l","l"]

#### Example 2
Input: ["cool","lock","cook"]
Output: ["c","o"]

---

### Note
1. 1 <= A.length <= 100
2. 1 <= A[i].length <= 100
3. A[i][j] is a lowercase letter

---

### Solution

```java
class Solution {
    public List<String> commonChars(String[] A) {
        List<String> result = new ArrayList<>();
        int[] commonCharsCount = new int[26];
        // fill the array with the max integer, so it can be compared with 
        Arrays.fill(commonCharsCount, Integer.MAX_VALUE);

        // iterate each string in A
        for (String s : A)
        {
            int[] tempCharsCount = new int[26];

            // count char in this string
            // index will be the sequence of each letter. eg: tempCharsCount[0] : a, tempCharsCount[1] : b
            for (Char c : s.toCharArray())
                tempCharsCount[c - 'a']++;

            // update the commonCharsCount
            // after iterate the string itself, compare with the common char array, 
            // it will get the min element from the array and reassign to the common char array
            for (int i = 0; i < commonCharsCount.length; i++)
                commonCharsCount[i] = Math.min(commonCharsCount[i], tempCharsCount[i]);
        }
        
        // iterate commonCharsCount to add each char
        // now the commonCharsCount has our result : the common elements will be marked as the count of the element
        // if the elements are not common, it will be 0 in the array
        for (int i = 0; i < commonCharsCount.length; i++)
        {
            while (commonCharsCount[i] > 0)
            {
                result.add("" + (char)('a' + i));
                commonCharsCount[i]--;
            }
        }

        return result;
    }
}

```