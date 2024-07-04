---
title: dynamic programming
description: dynamic programming
slug: dynamic programming
date: 2024-07-03
image: dp.jpg
categories:
    - leetcode
tags:
    - DP
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---
# 什么是动态规划
动态规划，英文：Dynamic Programming，简称DP，如果某一问题有很多重叠子问题，使用动态规划是最有效的。

所以动态规划中每一个状态一定是由上一个状态推导出来的，这一点就区分于贪心，贪心没有状态推导，而是从局部直接选最优的，

动态规划的解题步骤
做动规题目的时候，很多同学会陷入一个误区，就是以为把状态转移公式背下来，照葫芦画瓢改改，就开始写代码，甚至把题目AC之后，都不太清楚dp[i]表示的是什么。

这就是一种朦胧的状态，然后就把题给过了，遇到稍稍难一点的，可能直接就不会了，然后看题解，然后继续照葫芦画瓢陷入这种恶性循环中。

状态转移公式（递推公式）是很重要，但动规不仅仅只有递推公式。

**对于动态规划问题，我将拆解为如下五步曲，这五步都搞清楚了，才能说把动态规划真的掌握了！**

**1. 确定dp数组（dp table）以及下标的含义**

**2. 确定递推公式**

**3. dp数组如何初始化**

**4. 确定遍历顺序**

**5. 举例推导dp数组**
   
一些同学可能想为什么要先确定递推公式，然后在考虑初始化呢？

因为一些情况是递推公式决定了dp数组要如何初始化！

后面的讲解中我都是围绕着这五点来进行讲解。

可能刷过动态规划题目的同学可能都知道递推公式的重要性，感觉确定了递推公式这道题目就解出来了。

其实 确定递推公式 仅仅是解题里的一步而已！

一些同学知道递推公式，但搞不清楚dp数组应该如何初始化，或者正确的遍历顺序，以至于记下来公式，但写的程序怎么改都通过不了。

后序的讲解的大家就会慢慢感受到这五步的重要性了。

# 动态规划应该如何debug
相信动规的题目，很大部分同学都是这样做的。

看一下题解，感觉看懂了，然后照葫芦画瓢，如果能正好画对了，万事大吉，一旦要是没通过，就怎么改都通过不了，对 dp数组的初始化，递推公式，遍历顺序，处于一种黑盒的理解状态。

写动规题目，代码出问题很正常！

找问题的最好方式就是把dp数组打印出来，看看究竟是不是按照自己思路推导的！

# DP Questions List
[62. Unique Paths](https://kris0325.github.io/p/62.-unique-paths/)
[63. Unique Paths ii]()
[70. Climbing Stairs](https://kris0325.github.io/p/70.-climbing-stairs/)
[746. Min Cost Climbing Stairs](https://kris0325.github.io/p/746.-min-cost-climbing-stairs/)

