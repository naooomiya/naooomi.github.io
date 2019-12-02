---
title: '[LeetCode] 35. Search Insert Position'
date: 2019-11-23 17:48:22
tags: 
    - [Binary Search]
    - [LeetCode(Easy)]
categories: 
    - [LeetCode Easy]
    - [Binary Search]
---


### Description
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

<!-- more -->

---

#### Example 1
Input: [1,3,5,6], 5
Output: 2

#### Example 2
Input: [1,3,5,6], 2
Output: 1

#### Example 3
Input: [1,3,5,6], 7
Output: 4

#### Example 4
Input: [1,3,5,6], 0
Output: 0

---
### Solution

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        
        while (left <= right)
        {
            int pivot = left + (right - left) / 2;
            
            if (nums[pivot] == target) return pivot;
            else if (nums[pivot] > target) right = pivot - 1;
            else if (nums[pivot] < target) left = pivot + 1;
        }
        
        return left;
    }
}
```