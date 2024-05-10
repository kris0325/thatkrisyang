---
title: 349. Intersection of Two Arrays
description: 349. Intersection of Two Arrays

slug: 349. Intersection of Two Arrays

date: 2024-05-10
image: 349.png
categories:
    - leetcode
tags:
    - hash-table
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

> https://leetcode.com/problems/intersection-of-two-arrays/description/

```
Intersection of Two Arrays
Category	Difficulty	Likes	Dislikes
algorithms	Easy (74.44%)	5958	2289
Tags
hash-table | two-pointers | binary-search | sort

Companies
twosigma

Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must be unique and you may return the result in any order.

 

Example 1:

Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
Example 2:

Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
Explanation: [4,9] is also accepted.
 

Constraints:

1 <= nums1.length, nums2.length <= 1000
0 <= nums1[i], nums2[i] <= 1000

```

```Java
 /*
   思路：哈希表
        使用hashset存nums1的元素, 再遍历nums2收集intersection
  *
 */

// @lc code=start

import java.util.ArrayList;
import java.util.HashSet;

class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        HashSet<Integer> setNums1 = new HashSet<>();
        HashSet<Integer> setNums = new HashSet<>();
        for(int i = 0; i < nums1.length ; i++){
            setNums1.add(nums1[i]);
        }
        for(int i = 0; i < nums2.length; i++){
            if (setNums1.contains(nums2[i])) {
                setNums.add(nums2[i]);
            }
        }

        // int [] nums = new int[setNums.size()];
        // int index = 0;
        // for (int num : setNums) {
        //     nums[index++] = num;
        // }
        // return nums;
        return setNums.stream().mapToInt(i -> i).toArray();
    }
}
// @lc code=end

```