--- 
title:  213.HouseRobberII
description:  213.打家劫舍II

slug:  213.HouseRobberII

date: 2024-07-12
image: 213.png
categories:
    - Leetcode
tags:
    - DP
    - Medium
    - microsoft
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---


```java
/**
 * You are a professional robber planning to rob houses along a street. Each house
 * has a certain amount of money stashed. All houses at this place are arranged in
 * a circle. That means the first house is the neighbor of the last one. Meanwhile,
 * adjacent houses have a security system connected, and it will automatically
 * contact the police if two adjacent houses were broken into on the same night.
 * <p>
 * Given an integer array nums representing the amount of money of each house,
 * return the maximum amount of money you can rob tonight without alerting the police.
 * <p>
 * <p>
 * <p>
 * Example 1:
 * <p>
 * <p>
 * Input: nums = [2,3,2]
 * Output: 3
 * Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2)
 * , because they are adjacent houses.
 * <p>
 * <p>
 * Example 2:
 * <p>
 * <p>
 * Input: nums = [1,2,3,1]
 * Output: 4
 * Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
 * Total amount you can rob = 1 + 3 = 4.
 * <p>
 * <p>
 * Example 3:
 * <p>
 * <p>
 * Input: nums = [1,2,3]
 * Output: 3
 * <p>
 * <p>
 * <p>
 * Constraints:
 * <p>
 * <p>
 * 1 <= nums.length <= 100
 * 0 <= nums[i] <= 1000
 * <p>
 * <p>
 * Related Topics Array Dynamic Programming 👍 9805 👎 151
 */
       
/*
 2024-07-12 16:35:45

 House Robber II
Category	Difficulty	Likes	Dislikes
algorithms	Medium (41.96%)	9805	151
Tags
dynamic-programming

Companies
microsoft
*/
```
```java


class HouseRobberIi {
    public static void main(String[] args) {
        Solution solution = new HouseRobberIi().new Solution();
    }

    //leetcode submit region begin(Prohibit modification and deletion)
    class Solution {
        //DP: consider circle nums, nums[0], nums[length-1] are adjacent, so we can divide nums into two line new nums such as nums1: nums[0] -num[length-2] , nums2: nums[1] -num[length-1],
        // and get maximum = Math.max( rob(nums1), rob(nums2))
        //將環狀house，拆為線型house,讓首尾house不再相連，簡化問題，即将nums 拆分為2個數組， 從而把打家劫舍robII 转化为 打家劫舍rob
        public int rob(int[] nums) {
            if (nums == null || nums.length == 0) {
                return 0;
            }
            if (nums.length == 1) {
                return nums[0];
            }
            //從第一家開始打劫,直到nums[nums.length - 2], start to rob from the first house nums[0], so not consider to rob the last house nums[length-1]
            int robFromFirst = robLinear(nums, 0, nums.length - 2);
            //從第二家開始打劫，直到nums[nums.length - 1], start to rob from the second house num[1], so consider to rob the last house nums[length-1]
            int robFromSecond = robLinear(nums, 1, nums.length - 1);
            return Math.max(robFromFirst, robFromSecond);
        }

        public int robLinear(int[] nums, int start, int end) {
            if (start == end) {
                return nums[start];
            }
            int[] dp = new int[nums.length];
            dp[start] = nums[start];
            dp[start+1] = Math.max(nums[start], nums[start + 1]);
            for (int i = start + 2; i <= end; i++) {
                //dp[i] 可以分為 rob ｜ 不rob 當前stores[i]，取二者中的較大值
                dp[i] = Math.max(dp[i - 2] + nums[i], dp[i - 1]);
            }
            return dp[end];
        }

        private  int robLinear2(int[] houses, int start, int end) {
            if (start == end) {
                return houses[start];
            }
            int n = end - start + 1;
            int[] dp = new int[n];
            //注意处理初始化值，与dp[n]数组
            dp[0] = houses[start];
            dp[1] = Math.max(houses[start], houses[start + 1]);
            for (int i = 2; i < n; i++) {
                dp[i] = Math.max(dp[i - 1], dp[i - 2] + houses[start + i]);
            }
            return dp[n - 1];
        }
    }
//leetcode submit region end(Prohibit modification and deletion)

}
```