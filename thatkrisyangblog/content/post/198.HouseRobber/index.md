--- 
title:  198.HouseRobber
description:  198.HouseRobber

slug:  198.HouseRobber

date: 2024-07-15
image: 198.png
categories:
- Leetcode
tags:
- DP
- Medium
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

```java
/**
 * You are a professional robber planning to rob houses along a street. Each house
 * has a certain amount of money stashed, the only constraint stopping you from
 * robbing each of them is that adjacent houses have security systems connected and
 * it will automatically contact the police if two adjacent houses were broken into
 * on the same night.
 * <p>
 * Given an integer array nums representing the amount of money of each house,
 * return the maximum amount of money you can rob tonight without alerting the police.
 * <p>
 * <p>
 * <p>
 * Example 1:
 * <p>
 * <p>
 * Input: nums = [1,2,3,1]
 * Output: 4
 * Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
 * Total amount you can rob = 1 + 3 = 4.
 * <p>
 * <p>
 * Example 2:
 * <p>
 * <p>
 * Input: nums = [2,7,9,3,1]
 * Output: 12
 * Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (
 * money = 1).
 * Total amount you can rob = 2 + 9 + 1 = 12.
 * <p>
 * <p>
 * <p>
 * Constraints:
 * <p>
 * <p>
 * 1 <= nums.length <= 100
 * 0 <= nums[i] <= 400
 * <p>
 * <p>
 * Related Topics Array Dynamic Programming 👍 21014 👎 422
 */
     
 /*
 2024-07-12 15:20:03
*/

```

```java
   class Solution {
        public int rob(int[] nums) {
            return stealStore(nums);
        }

        public int stealStore(int[] stores) {
            if (stores == null || stores.length == 0) {
                return 0;
            }
            if (stores.length == 1) {
                return stores[0];
            }
            int[] dp = new int[stores.length];
            dp[0] = stores[0];
            dp[1] = Math.max(dp[0], stores[1]);
            for (int i = 2; i < stores.length; i++) {
                //dp[i] 可以分為 不rob ｜ rob 當前stores[i]，取二者中的較大值
                dp[i] = Math.max(dp[i - 1], dp[i - 2] + stores[i]);
                System.out.printf("i:%s,  dp[i]:%s ", i, dp[i]);
            }
            return dp[stores.length - 1];
        }
    }
```