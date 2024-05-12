--- 
title: 454. 4Sum II
description: 454. 4Sum II

slug: 454. 4Sum II

date: 2024-05-11
image: 454.png
categories:
    - leetcode
tags:
    - hashtable
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---


<https://leetcode.com/problems/4sum-ii/description/>

```
4Sum II
Category	Difficulty	Likes	Dislikes
algorithms	Medium (57.24%)	4879	140
Tags
hash-table | binary-search

Companies
Unknown

Given four integer arrays nums1, nums2, nums3, and nums4 all of length n, return the number of tuples (i, j, k, l) such that:

0 <= i, j, k, l < n
nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0
 

Example 1:

Input: nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]
Output: 2
Explanation:
The two tuples are:
1. (0, 0, 0, 1) -> nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1) + 0 = 0
Example 2:

Input: nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]
Output: 1
 

Constraints:

n == nums1.length
n == nums2.length
n == nums3.length
n == nums4.length
1 <= n <= 200
-228 <= nums1[i], nums2[i], nums3[i], nums4[i] <= 228

```

```
/**
  * 思路：哈希表
         條件 nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0， 可以拆分為
         (nums1[i] + nums2[j] )+  (nums2[j] + nums3[k]) == 0,
          还是 1. Two Sum（1.两数之和问题)
 */
```

```java
// @lc code=start
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        HashMap<Integer, Integer> fourSum = new HashMap<>();
        int count = 0;
        for(int i : nums1){
            for(int j : nums2){
                int sum = i +j;
                fourSum.put(sum, fourSum.getOrDefault(sum,0)+1);
            }
        }

        for(int k : nums3){
            for(int l : nums4){
                count += fourSum.getOrDefault((0-(k+l)), 0);
            }
        }
        return count;
    }
}
// @lc code=end

```