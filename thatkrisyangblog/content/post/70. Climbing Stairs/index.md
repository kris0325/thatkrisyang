---
title: 70. Climbing Stairs
description: 70. Climbing Stairs
slug: 70. Climbing Stairs
date: 2024-03-22
image: 70.png
categories:
    - leetcode
tags:
    - dp
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

```
/*
 * @lc app=leetcode.cn id=70 lang=java
 *
 * [70] 爬楼梯
 *
 * https://leetcode.cn/problems/climbing-stairs/description/
 *
 * algorithms
 * Easy (54.41%)
 * Likes:    3474
 * Dislikes: 0
 * Total Accepted:    1.4M
 * Total Submissions: 2.6M
 * Testcase Example:  '2'
 *
 * 假设你正在爬楼梯。需要 n 阶你才能到达楼顶。
 * 
 * 每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？
 * 
 * 
 * 
 * 示例 1：
 * 
 * 
 * 输入：n = 2
 * 输出：2
 * 解释：有两种方法可以爬到楼顶。
 * 1. 1 阶 + 1 阶
 * 2. 2 阶
 * 
 * 示例 2：
 * 
 * 
 * 输入：n = 3
 * 输出：3
 * 解释：有三种方法可以爬到楼顶。
 * 1. 1 阶 + 1 阶 + 1 阶
 * 2. 1 阶 + 2 阶
 * 3. 2 阶 + 1 阶
 * 
 * 
 * 
 * 
 * 提示：
 * 
 * 
 * 1 <= n <= 45
 * 
 * 
 */
 
```

```java
// @lc code=start
class Solution {
    public int climbStairs(int n) {
        if (n <= 2) {
            return n;
        }
        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        //注意下标index开始于i=3
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 2] + dp[i - 1];
            // System.out.println("dp[i]"+ "i:"+ i+":"+dp[i]);
        }
        return dp[n];
    }
}

// @lc code=end
```


```
 70. 爬楼梯（进阶版）
卡码网：57. 爬楼梯(opens new window)

假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬至多m (1 <= m < n)个台阶。你有多少种不同的方法可以爬到楼顶呢？
```
```java
之前讲这道题目的时候，因为还没有讲背包问题，所以就只是讲了一下爬楼梯最直接的动规方法（斐波那契）。

这次终于讲到了背包问题，我选择带录友们再爬一次楼梯！

这道题目 我们在动态规划：爬楼梯 中已经讲过一次了，这次我又给本题加点料，力扣上没有原题，所以可以在卡码网57. 爬楼梯 (opens new window)上来刷这道题目。

我们之前做的 爬楼梯 是只能至多爬两个台阶。

这次改为：一步一个台阶，两个台阶，三个台阶，.......，直到 m个台阶。问有多少种不同的方法可以爬到楼顶呢？

这又有难度了，这其实是一个完全背包问题。

1阶，2阶，.... m阶就是物品，楼顶就是背包。

每一阶可以重复使用，例如跳了1阶，还可以继续跳1阶。

问跳到楼顶有几种方法其实就是问装满背包有几种方法。

此时大家应该发现这就是一个完全背包问题了！

确定遍历顺序
这是背包里求排列问题，即：1、2 步 和 2、1 步都是上三个台阶，但是这两种方法不一样！
所以需将target放在外循环，将nums放在内循环。

每一步可以走多次，这是完全背包，内循环需要从前向后遍历
```

```java
public int climbStairs(int n, int m) {
    //定義dp數組: dp[j]表示爬上j層樓梯,每一次最大可爬m階樓梯，總共有多少中方法爬到j層
    int[] dp = new int[n + 1];
    //初始化dp[]
    dp[0] = 1;
    //遍歷順序
       //求排列問題，所以先遍歷背包，後遍歷物品
    for (int j = 1; j <= n; j++) {
        for (int i = 1; i <= m; i++) {
            //每次選擇爬的層數i不能超過樓梯總層數j
            if (j >= i) {
                //遞推公式
                dp[j] += dp[j - j];
            }
        }
    }
    return dp[n];
}

```


