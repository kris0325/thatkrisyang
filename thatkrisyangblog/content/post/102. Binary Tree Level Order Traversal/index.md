--- 
title:  102. Binary Tree Level Order Traversal
description:  102. Binary Tree Level Order Traversal

slug:  102. Binary Tree Level Order Traversal

date: 2024-06-09
image: 102.png
categories:
    - leetcode
    - Binary Tree
tags:
    - Binary Tree
    - Queue
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

```
Binary Tree Level Order Traversal
Category	Difficulty	Likes	Dislikes
algorithms	Medium (67.15%)	15149	309
Tags
tree | breadth-first-search

Companies
amazon | apple | bloomberg | facebook | linkedin | microsoft

Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

 

Example 1:


Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
Example 2:

Input: root = [1]
Output: [[1]]
Example 3:

Input: root = []
Output: []
 

Constraints:

The number of nodes in the tree is in the range [0, 2000].
-1000 <= Node.val <= 1000

 https://leetcode.com/problems/binary-tree-level-order-traversal/description/
 *

 /*
 * 思路：二叉树层序遍历，借助queue辅助数据结构来实现
 * */
```



```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    public List<List<Integer>> levelOrder(TreeNode root) {
        if(null == root) {
            return result;
        }
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            //收集当前level的节点元素
            List<Integer> list = new ArrayList<>();
            //记录当前节点数量
            int len = queue.size();
            //遍历当前level
            for(int i = 0; i < len;i++){
                TreeNode node = queue.poll();  
                list.add(node.val);
                if(node.left != null){
                    queue.offer(node.left);
                }
                if(node.right != null){
                    queue.offer(node.right);
                }
            }
            result.add(list);
        }
        return result;
    }
}
```

