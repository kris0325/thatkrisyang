---
title: 209. Minimum Size Subarray Sum
description: 209. Minimum Size Subarray Sum
slug: 209. Minimum Size Subarray Sum
date: 2024-03-25
image: 209.png
categories:
  - leetcode
tags:
  - array
  - two-pointers
  - binary-search
  - sliding window
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

```
/*
 * @lc app=leetcode.cn id=209 lang=java
 *
 * [209] 长度最小的子数组
 *
 * https://leetcode.cn/problems/minimum-size-subarray-sum/description/
 *
 * algorithms
 * Medium (46.41%)
 * Likes:    2088
 * Dislikes: 0
 * Total Accepted:    727.9K
 * Total Submissions: 1.6M
 * Testcase Example:  '7\n[2,3,1,2,4,3]'
 *
 * 给定一个含有 n 个正整数的数组和一个正整数 target 。
 * 
 * 找出该数组中满足其总和大于等于 target 的长度最小的 连续子数组 [numsl, numsl+1, ..., numsr-1, numsr]
 * ，并返回其长度。如果不存在符合条件的子数组，返回 0 。
 * 
 * 
 * 
 * 示例 1：
 * 
 * 
 * 输入：target = 7, nums = [2,3,1,2,4,3]
 * 输出：2
 * 解释：子数组 [4,3] 是该条件下的长度最小的子数组。
 * 
 * 
 * 示例 2：
 * 
 * 
 * 输入：target = 4, nums = [1,4,4]
 * 输出：1
 * 
 * 
 * 示例 3：
 * 
 * 
 * 输入：target = 11, nums = [1,1,1,1,1,1,1,1]
 * 输出：0
 * 
 * 
 * 
 * 
 * 提示：
 * 
 * 
 * 1 <= target <= 10^9
 * 1 <= nums.length <= 10^5
 * 1 <= nums[i] <= 10^5
 * 
 * 
 * 
 * 
 * 进阶：
 * 
 * 
 * 如果你已经实现 O(n) 时间复杂度的解法, 请尝试设计一个 O(n log(n)) 时间复杂度的解法。
 * 
 * 
 * 
 * 思路：滑动窗口
 * 快慢指针移动形成滑动窗口，进行判断窗口值之和是否满足条件，再通过快慢指针移动推动滑动窗口
 */

// @lc code=start
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int reslut = Integer.MAX_VALUE;
        //滑动窗口数组值之和
        int sum = 0;
        //左边慢指针即滑动窗口起始位置
        int slow = 0;
        //滑动窗口的长度
        int subLength =0;
        //右边快指针即滑动窗口结束位置
        for(int fast = 0; fast < nums.length;fast++){
            sum += nums[fast];
            //当每次循环判断滑动窗口的截断出的数组值之和sum满足条件时， 进行比较并更新滑动窗口长度 subLength，
            //然后下一次循环，先更新sum，后更新向右移动慢指针，
            while (sum >= target) {
                subLength = fast -slow + 1;
                reslut = Math.min(reslut, subLength );
                // sum -= nums[slow++];
                //sum -= nums[slow++];注意顺序，即：
                sum -= nums[slow];
                slow ++;
            }
        }
        return reslut == Integer.MAX_VALUE? 0 : reslut;
    }
}

// @lc code=end



```

```
英文题目描述
Maximum Average Stock Price

The price of Amazon common stock is analyzed over a period of several months.
 A group of k consecutive months is said to be observable if no two months in the group have the same stock price. 
 In other words, all the prices in the period are distinct. 
 The sum of stock prices of an observable group of months is called the cumulative observable sum.
  Given the price of Amazon stock for n months, find the maximum possible cumulative observable sum among all the observable groups of months.
   If there is no observable group, return -1.

Example

Input:
stockPrices = [1, 2, 7, 7, 4, 3, 6]
k = 3
Output: 14
中文题目描述
最大平均股票价格

亚马逊普通股票的价格在几个月内进行了分析。
如果一组连续的k个月没有两个月份的股票价格相同，则称该组是可观测的。
换句话说，该期间内所有价格都是不同的。一组可观测月份的股票价格总和称为累计可观测总和。
给定亚马逊股票几个月的价格，找出所有可观测月份组中可能的最大累计可观测总和。
如果没有可观测组，则返回-1。
```

```java
import java.util.HashSet;//sliding window question：滑動窗口 + hashset維護數組，保證沒有重複元素， 更新求和

public int maximumConsecutiveStockPrice(int[] arr, int k) {
    int start = 0;
    int end = 0;
    HashSet<Integer> stockSet = new HashSet<>();
    int currentSum = 0;
    int maxSum = -1;
    if (arr == null || arr.length < k) {
        return -1;
    }
    while (end < arr.length) {
        //發現重複元素時，循環移除arr[start]元素，並向右移動start指針，直到當前子數組沒有重複元素
        while (stockSet.contains(arr[end])) {
            stockSet.remove(arr[start]);
            currentSum -= arr[start];
            start++;
        }
        //移動end，加入子數組
        currentSum += arr[end];
        stockSet.add(arr[end]);

        if (end - start + 1 == k) {
            //子數組滿足k時，更新maxSum，同時向右移動窗口一步
            maxSum = Math.max(maxSum, currentSum);
            stockSet.remove(arr[start]);
            start++;
            end++;
        }
        return maxSum;
    }
}
```

```
Get Minimum Boxes

The supply chain manager at one of Amazon's warehouses is shipping the last container of the day. All n boxes have been loaded into the truck with their sizes represented in the array boxes. The truck may not have enough capacity to store all the boxes though, so some of the boxes may have to be unloaded. The remaining boxes must satisfy the condition max(boxes) ≤ capacity * min(boxes).

Given the array, boxes, and capacity, find the minimum number of boxes that need to be unloaded.

Function Description

Complete the function getMinimumBoxes in the editor.

getMinimumBoxes has the following parameters:

1. int[] boxes: an array of integers representing the sizes of the boxes
2. int capacity: the capacity of the truck
Returns

int: the minimum number of boxes that need to be unloaded

Example 1:
Input:  boxes = [1, 4, 3, 2], capacity = 2
Output: 1 
Explanation: remove arr[0] =1,
```

```java
//greedy 
//sliding window
// max(boxes) ≤ capacity * min(boxes)的物理意义：
//capacity：一个预定的容量系数，在某些情况下，可能需要确保重量分布较为均匀，以避免某些箱子过重而其他箱子过轻。公式 max(boxes) ≤ capacity * min(boxes) 强制要求最大的箱子重量不超过最小箱子重量的 capacity 倍，这样就可以控制各个箱子之间的重量差异，避免出现重量差异过大的情况。
// 1 运输为平衡负载方便搬运与运输，
// 2 优化利用空间重量size差异过大会导致空间利用率不高，
// 3 安全性：在某些应用场景下，过重的箱子可能会带来安全隐患，
//  通过这个公式可以确保每个箱子的重量在合理范围内。

//先排序，排序后，才能方便的高效的计算箱子最大值和最小值的比值，如何和capacity比较
//greedy question：
// 局部最优选择：在排序后，每次选择当前窗口中最大的子数组，确保最大值和最小值的比值不超过 capacity。我们不断调整窗口的大小来找到最优的局部解。
//全局最优目标：通过不断调整窗口来寻找所有可能的子数组，最终找到需要卸载最少箱子的方案。

import java.util.Arrays;// 求最大maxBox/minBox  < capacity,

public int getMinimumBoxes(int[] boxes, int capacity) {
    int length = boxes.length;
    int minUpload = length;
    int left = 0;

    //1.排序：首先对箱子的尺寸数组排序
    Arrays.sort(boxes);
    //2.滑动窗口:使用双指针来來找滿足條件的最大子數組
    for (int right = 0; right < length; right++) {
        while (boxes[right] > capacity * boxes[left]) {
            //1.不滿足條件時，left指針右移動，upload左邊的箱子
            left++;
        }
        //2.滿足條件，每次都更新計算子數組的最小upload數，然後right指針右移動，load增加箱子
        //minUpload = min(minUpload,左邊upload的箱子+右邊upload的箱子數)
        //3.計算中更新最小卸載數量
        minUpload = Math.min(minUpload, left + (length - 1 - right));
    }
    return minUpload;
}


```

