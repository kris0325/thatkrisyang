---
title: 236.lowest-common-ancestor-of-a-binary-tree.java
description: 236.lowest-common-ancestor-of-a-binary-tree.java

slug: 236.lowest-common-ancestor-of-a-binary-tree.java

date: 2024-06-23
# image: 142.png
categories:
    - leetcode
    - Binary Tree
tags:
    - DFS
    - Medium
    - amazon 
    - apple 
    - facebook 
    - linkedin 
    - microsoft
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

```
Lowest Common Ancestor of a Binary Tree
Category	Difficulty	Likes	Dislikes
algorithms	Medium (62.14%)	16387	409
Tags
tree

Companies
amazon | apple | facebook | linkedin | microsoft

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

 

Example 1:


Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
Example 2:


Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
Example 3:

Input: root = [1,2], p = 1, q = 2
Output: 1
 

Constraints:

The number of nodes in the tree is in the range [2, 105].
-109 <= Node.val <= 109
All Node.val are unique.
p != q
p and q will exist in the tree.
```

```java
class Solution {
          public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
              if (root == null || root == p || root == q) { // 递归结束条件
                  return root;
              }
              // 后序遍历
              TreeNode left = lowestCommonAncestor(root.left, p, q);
              TreeNode right = lowestCommonAncestor(root.right, p, q);

              if(left == null && right == null) { // 若未找到节点 p 或 q
                  return null;
              }else if(left == null && right != null) { // 若找到一个节点
                  return right;
              }else if(left != null && right == null) { // 若找到一个节点
                  return left;
              }else { // 若找到两个节点
                  return root;
              }
          }
      }
```