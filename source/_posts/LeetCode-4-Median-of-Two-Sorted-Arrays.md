---
title: '[LeetCode] 4. Median of Two Sorted Arrays'
date: 2019-11-18 23:31:42
tags: 
    - Binary Search
    - LeetCode(Hard)
categories: 
    - [LeetCode Hard]
    - [Binary Search]
---


### Description
There are two sorted arrays **nums1** and **nums2** of size m and n respectively.
Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).
You may assume **nums1** and **nums2** cannot be both empty.

<!-- more -->

#### Example 1
nums1 = [1, 3]  
nums2 = [2]

The median is 2.0

#### Example 2
nums1 = [1, 2]  
nums2 = [3, 4]  

The median is (2 + 3)/2 = 2.5

---
### Solution

Find the median of two sorted arrays:

eg.
arr1 = [1, 3, 5]
arr2 = [2, 4, 6]

[1, 2, 3, 4, 5, 6] (merge in a sorted order)

median(arr1, arr2) = (3+4) / 2 = 3.5 

There are some questions we need to consider. In this case, the problem definition doesn't specify that the two arrays are the same length. If it's not the same length, we need to do it in a clever way. Second, the arrays are arrays of integers and we're going to return a double in this case because we're doing an average.

Normal way:
Merge two arrays into one sorted array and it will take linear time. The median will be the middle element(size is odd) or the average of middle two elements(size is even). 

Another example:
arr1 = [1, 2, 3, 4, 5, 6]
Median: 3.5

arr2 = [0, 0, 0, 0, 10, 10]
Median: 0

We can see that the median of the first array is bigger than the second array, that means that the first array must have more elements on the high side than the second array. So we can find that the median of the first arrays must be in the lesser half of the array. And for the second array, the median must be in the greater half of the array. Otherwise the medians would be equal. This means both arrays have the same spacing of the elements on either side of the median. And if the median is the same for both array, the median for both array stay the same.  

[To Be Continue]