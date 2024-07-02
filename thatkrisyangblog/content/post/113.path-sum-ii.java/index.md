---
title: 113.path-sum-ii.java
description: 113.path-sum-ii.java

slug: 113.path-sum-ii.java

date: 2024-06-23
# image: 142.png
categories:
    - leetcode
    - Binary Tree
tags:
    - DFS
    - Tree
    - bloomberg
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

```
Path Sum II
Category	Difficulty	Likes	Dislikes
algorithms	Medium (58.45%)	7918	154
Tags
tree | depth-first-search

Companies
bloomberg

Given the root of a binary tree and an integer targetSum, return all root-to-leaf paths where the sum of the node values in the path equals targetSum. Each path should be returned as a list of the node values, not node references.

A root-to-leaf path is a path starting from the root and ending at any leaf node. A leaf is a node with no children.

 

Example 1:


Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: [[5,4,11,2],[5,8,4,5]]
Explanation: There are two paths whose sum equals targetSum:
5 + 4 + 11 + 2 = 22
5 + 8 + 4 + 5 = 22
Example 2:


Input: root = [1,2,3], targetSum = 5
Output: []
Example 3:

Input: root = [1,2], targetSum = 0
Output: []
 

Constraints:

The number of nodes in the tree is in the range [0, 5000].
-1000 <= Node.val <= 1000
-1000 <= targetSum <= 1000
```

```java
class Solution {

    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> pathList = new ArrayList<>();
        List<Integer> path = new ArrayList<>();
        if(null == root){
            return pathList;
        }
        backtracking(root, targetSum, pathList, path);
        return pathList;
    }

    public void backtracking(TreeNode node
    , int targetSum, List<List<Integer>> pathList
    , List<Integer> path){

        //添加当前节点
        path.add(node.val);
        // leaf node
        if(node.left == null && node.right == null){
           if(path.stream()
                   .mapToInt(Integer::intValue)
                   .sum() == targetSum){
                    //path是应用对象，所以不能直接pathList.add(path)，需要拷贝后再add
                       pathList.add(new ArrayList<>(path));
              }
         //回溯
          path.remove(path.size()-1); 
          //返回上一层调用
          return;
        }

        /**
         * 遍历左右2个节点
        * for(int i =0； i<2; i++ )
        * 遍历完后，再回溯
       */
        //遍历left
        if(null != node.left){
            backtracking(node.left, targetSum, pathList, path);
        }
        //遍历right
        if(null != node.right){
            backtracking(node.right, targetSum, pathList, path);
        }

        //在处理完当前节点的左右子节点后进行回溯
        path.remove(path.size()-1);
    }
}
```