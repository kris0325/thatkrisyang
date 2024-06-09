--- 
title:  144.binary-tree-preorder-traversal.java
description:  144.binary-tree-preorder-traversal.java

slug:  144.binary-tree-preorder-traversal.java

date: 2024-06-08
image: 144.png
categories:
    - leetcode
    - Binary Tree
tags:
    - Binary Tree
    - Stack
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

<https://leetcode.com/problems/binary-tree-postorder-traversal/description/>

```
/*
 * @lc app=leetcode id=144 lang=java
 *
 * [144] Binary Tree Preorder Traversal
 *
 * https://leetcode.com/problems/binary-tree-preorder-traversal/description/
 *
 * algorithms
 * Easy (69.46%)
 * Likes:    7911
 * Dislikes: 209
 * Total Accepted:    1.6M
 * Total Submissions: 2.3M
 * Testcase Example:  '[1,null,2,3]'
 *
 * Given the root of a binary tree, return the preorder traversal of its nodes'
 * values.
 * 
 * 
 * Example 1:
 * 
 * 
 * Input: root = [1,null,2,3]
 * Output: [1,2,3]
 * 
 * 
 * Example 2:
 * 
 * 
 * Input: root = []
 * Output: []
 * 
 * 
 * Example 3:
 * 
 * 
 * Input: root = [1]
 * Output: [1]
 * 
 * 
 * 
 * Constraints:
 * 
 * 
 * The number of nodes in the tree is in the range [0, 100].
 * -100 <= Node.val <= 100
 * 
 * 
 * 
 * Follow up: Recursive solution is trivial, could you do it iteratively?
 * 
 */



```


```java
/*
* 思路：遞歸實現
*/
class Solution1 {
    List<Integer> result = new ArrayList<>();
    
    public List<Integer> preorderTraversal(TreeNode root) {
        if(null == root){
            return result;
        }
        result.add(root.val);
        preorderTraversal(root.left);
        preorderTraversal(root.right);
        return result;
    }

}

/*
* 思路：迭代實現
*/
class Solution {
    List<Integer> result = new ArrayList<>();

    public List<Integer> preorderTraversal(TreeNode root) {
        if (null == root) {
            return result;
        }
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            result.add(node.val);
            if (node.right != null) {
                stack.push(node.right);
            }
            if (node.left != null) {
                stack.push(node.left);
            }
        }
        return result;

    }

}

// @lc code=end



```