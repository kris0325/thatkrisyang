---
title: 108.convert-sorted-array-to-binary-search-tree.java
description: 108.convert-sorted-array-to-binary-search-tree.java

slug: 108.convert-sorted-array-to-binary-search-tree.java

date: 2024-06-23
# image: 142.png
categories:
    - leetcode
    - Binary Tree
tags:
    - DFS
    - Tree
    - airbnb
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---
```
Convert Sorted Array to Binary Search Tree
Category	Difficulty	Likes	Dislikes
algorithms	Easy (71.65%)	10921	556
Tags
tree | depth-first-search

Companies
airbnb

Given an integer array nums where the elements are sorted in ascending order, convert it to a height-balanced binary search tree.

 

Example 1:


Input: nums = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: [0,-10,5,null,-3,null,9] is also accepted:

Example 2:


Input: nums = [1,3]
Output: [3,1]
Explanation: [1,null,3] and [3,1] are both height-balanced BSTs.
 

Constraints:

1 <= nums.length <= 104
-104 <= nums[i] <= 104
nums is sorted in a strictly increasing order.
```


```java
    class Solution {
        // 二分法，获取有序数组中间节点为根节点，以中间节点作为切割点，然后再递归左数组，右数组
        public TreeNode sortedArrayToBST(int[] nums) {
           return sortedArrayToBST(nums, 0, nums.length - 1);
        }
        public TreeNode sortedArrayToBST(int[] nums, int left, int right) {
            if (left > right) return null;
            int mid = left + (right - left) / 2;
            TreeNode current = new TreeNode(nums[mid]);
            current.left = sortedArrayToBST(nums, left, mid - 1);
            current.right = sortedArrayToBST(nums, mid + 1, right);
            return current;
        }
    }
```