--- 
title:  122.BestTimeToBuyAndSellStock II
description:  122.買賣股票的最佳時機 II

slug:  122.BestTimeToBuyAndSellStock II

date: 2024-07-03

image: 122.png

categories:
    - Leetcode
tags:
    - DP
    - Medium
weight: 1 # You can add weight to some posts to override the default sorting (date descending)
---

```java
/**
 * You are given an integer array prices where prices[i] is the price of a given
 * stock on the iᵗʰ day.
 * <p>
 * On each day, you may decide to buy and/or sell the stock. You can only hold at
 * most one share of the stock at any time. However, you can buy it then
 * immediately sell it on the same day.
 * <p>
 * Find and return the maximum profit you can achieve.
 * <p>
 * <p>
 * Example 1:
 * <p>
 * <p>
 * Input: prices = [7,1,5,3,6,4]
 * Output: 7
 * Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-
 * 1 = 4.
 * Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
 * Total profit is 4 + 3 = 7.
 * <p>
 * <p>
 * Example 2:
 * <p>
 * <p>
 * Input: prices = [1,2,3,4,5]
 * Output: 4
 * Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-
 * 1 = 4.
 * Total profit is 4.
 * <p>
 * <p>
 * Example 3:
 * <p>
 * <p>
 * Input: prices = [7,6,4,3,1]
 * Output: 0
 * Explanation: There is no way to make a positive profit, so we never buy the
 * stock to achieve the maximum profit of 0.
 * <p>
 * <p>
 * <p>
 * Constraints:
 * <p>
 * <p>
 * 1 <= prices.length <= 3 * 10⁴
 * 0 <= prices[i] <= 10⁴
 * <p>
 * <p>
 * Related Topics Array Dynamic Programming Greedy 👍 13507 👎 2694
 */
       
/*
 2024-07-03 17:02:18
 Best Time to Buy and Sell Stock II
Category	Difficulty	Likes	Dislikes
algorithms	Medium (66.40%)	13507	2694
Tags
array | greedy

Companies
bloomberg
*/
```

```java
    //leetcode submit region begin(Prohibit modification and deletion)
class Solution1 {
    //greedy algorithm： 價格低時買入，價格高時賣出，
    //要求局部最優解，那麼可以每天都交易，然後算出每天的profit，price[i] -price[i-1], 只收集正利潤即可
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        for (int i = 1; i < prices.length; i++) {
            //只收集正利潤
            maxProfit += Math.max(prices[i] - prices[i - 1], 0);
        }
        return maxProfit;
    }
}


class Solution {
    //DP algorithm： 價格低時買入，價格高時賣出，
    public int maxProfit(int[] prices) {
        int[][] dp = new int[prices.length][2];
        //dp[i][0] 第i天持有股票後的最多現金
        //dp[i][1] 第i天持有的最多現金(前一天賣掉股票)

        //第0天買入股票，開始現金為0,那麼買入股票後的現金就是-prices[0]，所以是一個負數
        dp[0][0] = -prices[0];
        int n = prices.length;
        for (int i = 1; i < n; i++) {
            //第i天持有股票後的最多現金 = max(保持第i-1天的狀態不變 即第i - 1天持有股票後的最多現金, 第i-1天持有的最多現金-買第i天股票的錢）
            dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1] - prices[i]);
            //第i天持有的最多現金 = max(第i-1天持有的最多現金, 第i-1天持有股票後的最多現金+賣第i天股票的錢)
            dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] + prices[i]);
        }
        return Math.max(dp[n - 1][0], dp[n - 1][1]);
    }
}
//leetcode submit region end(Prohibit modification and deletion)
```