---
title: 39.combination-sum
description: 39.combination-sum
slug: 39.combination-sum
date: 2024-01-25
# image: 90.jpg
categories:
    - leetcode
tags:
    - combination
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

```
/*
 * @lc app=leetcode id=39 lang=java
 *
 * [39] Combination Sum
 *
 * https://leetcode.com/problems/combination-sum/description/
 *
 * algorithms
 * Medium (70.32%)
 * Likes:    17899
 * Dislikes: 367
 * Total Accepted:    1.7M
 * Total Submissions: 2.4M
 * Testcase Example:  '[2,3,6,7]\n7'
 *
 * Given an array of distinct integers candidates and a target integer target,
 * return a list of all unique combinations of candidates where the chosen
 * numbers sum to target. You may return the combinations in any order.
 * 
 * The same number may be chosen from candidates an unlimited number of times.
 * Two combinations are unique if the frequency of at least one of the chosen
 * numbers is different.
 * 
 * The test cases are generated such that the number of unique combinations
 * that sum up to target is less than 150 combinations for the given input.
 * 
 * 
 * Example 1:
 * 
 * 
 * Input: candidates = [2,3,6,7], target = 7
 * Output: [[2,2,3],[7]]
 * Explanation:
 * 2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple
 * times.
 * 7 is a candidate, and 7 = 7.
 * These are the only two combinations.
 * 
 * 
 * Example 2:
 * 
 * 
 * Input: candidates = [2,3,5], target = 8
 * Output: [[2,2,2,2],[2,3,3],[3,5]]
 * 
 * 
 * Example 3:
 * 
 * 
 * Input: candidates = [2], target = 1
 * Output: []
 * 
 * 
 * 
 * Constraints:
 * 
 * 
 * 1 <= candidates.length <= 30
 * 2 <= candidates[i] <= 40
 * All elements of candidates are distinct.
 * 1 <= target <= 40
 * 
 * 
 *  * @param candidates 候选数组
     * @param begin      搜索起点
     * @param len        冗余变量，是 candidates 里的属性，可以不传
     * @param target     每减去一个元素，目标值变小
     * @param cur       从根结点到叶子结点的路径，是一个栈
     * @param res        结果集列表

   参考链接：https://leetcode.cn/problems/combination-sum/solutions/14697/hui-su-suan-fa-jian-zhi-python-dai-ma-java-dai-m-2/
 * 
 * 对于所有搜素可行解类型的问题，都可以尝试 “搜索回溯”的方法求解
 * solution1 
 * 深度优先搜索算法
 * 
 * 
 * 剪枝提速
根据上面画树形图的经验，如果 target 减去一个数得到负数，那么减去一个更大的树依然是负数，同样搜索不到结果。基于这个想法，我们可以对输入数组进行排序，添加相关逻辑达到进一步剪枝的目的；
排序是为了提高搜索速度，对于解决这个问题来说非必要。但是搜索问题一般复杂度较高，能剪枝就尽量剪枝。实际工作中如果遇到两种方案拿捏不准的情况，都试一下。
 * solution2 
 * 1 先排序，剪枝
 * 2 再使用深度优先搜索算法
 */

// @lc code=start

import java.lang.reflect.Array;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Deque;

class Solution1 {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> combinations = new ArrayList<>();
        int length = candidates.length;
        Deque<Integer> cur = new ArrayDeque<>();
        if(length==0){
            return combinations;
        }
        dfs(candidates,target,0,length,combinations,cur);
        return combinations;
    }


        public void dfs(int[] candidates, int target,  int begin, int length, List<List<Integer>> combinations, Deque<Integer> cur ){
            if(target <0){
                return;
            }
            if(target == 0){
               combinations.add(new ArrayList(cur)); 
               return;
            }
            // 重点理解这里从 begin 开始搜索的语意
            for (int i = begin; i < length; i++){
                cur.addLast(candidates[i]);
                 // 注意：由于每一个元素可以重复使用，下一轮搜索的起点依然是 i，而不是i+1，这里非常容易弄错
                dfs(candidates,target-candidates[i], i, length,combinations,cur);
                // 状态重置
                cur.removeLast();
            }

        }
}



class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> combinations = new ArrayList<>();
        int length = candidates.length;
        // 排序是剪枝的前提
        Arrays.sort(candidates); 
        Deque<Integer> cur = new ArrayDeque<>();
        if(length==0){
            return combinations;
        }
        dfs(candidates,target, 0, length,combinations,cur);
        return combinations;
    }


        public void dfs(int[] candidates, int target, int begin, int length, List<List<Integer>> combinations, Deque<Integer> cur ){
            // 由于进入更深层的时候，小于 0 的部分被剪枝，因此递归终止条件值只判断等于 0 的情况
            if(target == 0){
               combinations.add(new ArrayList(cur)); 
               return;
            }
            for (int i = begin; i < length; i++){
                
                if(target < candidates[i]) {
                    break;
                }
                cur.addLast(candidates[i]);
                dfs(candidates,target-candidates[i], i, length,combinations,cur);
                cur.removeLast();
            }

        }
}


// @lc code=end


```