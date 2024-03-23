---
title: 704. Binary Search
description: 排序数组找target，可以使用单指针进行二分搜索
slug: 704. Binary Search
date: 2024-03-23
image: 704.png
categories:
    - leetcode
tags:
    - ARRAY
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

```
/*
 * @lc app=leetcode.cn id=704 lang=java
 *
 * [704] 二分查找
 *
 * https://leetcode.cn/problems/binary-search/description/
 *
 * algorithms
 * Easy (55.14%)
 * Likes:    1551
 * Dislikes: 0
 * Total Accepted:    1.2M
 * Total Submissions: 2.2M
 * Testcase Example:  '[-1,0,3,5,9,12]\n9'
 *
 * 给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的
 * target，如果目标值存在返回下标，否则返回 -1。
 * 
 * 
 * 示例 1:
 * 
 * 输入: nums = [-1,0,3,5,9,12], target = 9
 * 输出: 4
 * 解释: 9 出现在 nums 中并且下标为 4
 * 
 * 
 * 示例 2:
 * 
 * 输入: nums = [-1,0,3,5,9,12], target = 2
 * 输出: -1
 * 解释: 2 不存在 nums 中因此返回 -1
 * 
 * 
 * 
 * 
 * 提示：
 * 
 * 
 * 你可以假设 nums 中的所有元素是不重复的。
 * n 将在 [1, 10000]之间。
 * nums 的每个元素都将在 [-9999, 9999]之间。
 * 
 * 思路：排序数组找target，可以使用单指针进行二分搜索
 */

// @lc code=start
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length -1;
        while (left <= right) {
            int middle = left + (right -left)/2;
            //target在左区间
            if(target < nums[middle]){
                //middle指针下标需要向左边移动时，避免2个元素数组的case下标不移动，所以需要-1
                right = middle -1;
                
            } else if(target > nums[middle]){
                //target在右区间
                //同理，middle指针向右移动时，下标需要+1，
                left = middle +1;
            } else{
                return middle;
            }            
        }

        return -1;
    }
}
// @lc code=end


```