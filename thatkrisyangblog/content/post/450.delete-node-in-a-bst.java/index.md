---
title: 450.delete-node-in-a-bst.java
description: 450.delete-node-in-a-bst.java 

slug: 450.delete-node-in-a-bst.java

date: 2024-06-23
# image: 142.png
categories:
    - leetcode
    - Binary Tree
tags:
    - DFS
    - uber 
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---


```
Delete Node in a BST
Category	Difficulty	Likes	Dislikes
algorithms	Medium (51.20%)	9042	276
Tags
Companies
uber

Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:

Search for a node to remove.
If the node is found, delete the node.
 

Example 1:


Input: root = [5,3,6,2,4,null,7], key = 3
Output: [5,4,6,2,null,null,7]
Explanation: Given key to delete is 3. So we find the node with value 3 and delete it.
One valid answer is [5,4,6,2,null,null,7], shown in the above BST.
Please notice that another valid answer is [5,2,6,null,4,null,7] and it's also accepted.

Example 2:

Input: root = [5,3,6,2,4,null,7], key = 0
Output: [5,3,6,2,4,null,7]
Explanation: The tree does not contain a node with value = 0.
Example 3:

Input: root = [], key = 0
Output: []
 

Constraints:

The number of nodes in the tree is in the range [0, 104].
-105 <= Node.val <= 105
Each node has a unique value.
root is a valid binary search tree.
-105 <= key <= 105
 

Follow up: Could you solve it with time complexity O(height of tree)?
```

```java

    class Solution {
        //solution:.简化版递归
        //1).确定终止条件：if(root == null), return root;

        //2).单层递归逻辑
        //case1. 没找到要删除的目标节点，遍历到空节点，直接return null

        //找到要删除的目标节点,处理当前节点:
        //case2. 当前节点左，右孩子都为null, 直接删除当前节点，return null
        //case3.  当前节点左孩子为null cur.left == null, 则返回右孩子return cur.right
        //case4. 当前节点右孩子为null cur.right == null, 则返回左孩子return cur.left
        //case5. 当前节点左，右孩子都不为null,
        //1 先遍历当前节点的右孩子cur.right 的最左边的“最左叶子节点”，将单前节点的左孩子cur.left放在“最左叶子节点”的左孩子位置
        //2 再将则返回当前节点的右孩子cur.right

        //key < root.val,递归处理左边节点（如过有左节点的话，处理后用左节点接住返回的结果
        //key > root.val,递归处理右边节点（如果有的话，处理后用左节点接住返回的结果
        //return root
        public TreeNode deleteNode(TreeNode root, int key) {
            if (root == null) {
                return null;
            }
            if (root.val == key) {
                // case1. 和case5. 可以合并为 else 来处理
//                if (root.left == null && root.right == null) {
//                    return null;
//                } else
                    if (root.left == null) {
                    return root.right;
                } else if (root.right == null) {
                    return root.left;
                } else {
                    TreeNode cur = root.right;
                    while (cur.left != null) {
                        cur = cur.left;
                    }
                    cur.left = root.left;
                    root = root.right;
                    return root;
                }
            }
            if (key < root.val) {
                root.left = deleteNode(root.left, key);
            }
            if (key > root.val) {
                root.right = deleteNode(root.right, key);
            }
            return root;
        }
    }
```

```java
class Solution2 {
        //solution:2.递归
        public TreeNode deleteNode(TreeNode root, int key) {
            if (root == null) {
                return null;
            }
            TreeNode parrent = null;
            TreeNode current = root;
            while (current != null) {
                if (current.val < key){
                    // right tree
                    parrent = current;
                    current = current.right;
                } else if (current.val > key) {
                    //left tree
                    parrent = current;
                    current = current.left;
                }else {
                    //find the key node
                    break;
                }

                //以下代码有BUG: 全部情况只有==，>, <3种case， 每种情况是互斥的，但是每个if之间少了else，执行完一种case判断后，应该直接跳到while（current != null）开头进行判断，
                // 但少了else，
                // 就继续往下执行了，所以是有问题的，而且 parrent没有及时更新，而且可能出现 null空指针异常，
                // test case [5,3,8,null，null,6,10], key == 7的情况，是会报null空指针异常的
//                if (current.val == key) {
//                    // find the key node
//                    break;
//                }
//                parrent = current;
//                if (current.val < key) {
//                    current = current.right;
//                }
//                if (current.val > key) {
//                    current = current.left;
//                }
            }
            //BSF只有一个节点
            if (parrent == null) {
                return deletOneNode(current);
            }
            // key 在 left
            if (parrent.left != null && key == parrent.left.val) {
                parrent.left = deletOneNode(current);
            }
            //key 在 right
            if (parrent.right != null && key == parrent.right.val) {
                parrent.right = deletOneNode(current);
            }
            //return root 也包含了  没找BSF does not contain key,此时  ,current == null jump out while loop
//            if (current == null) {
//                return root;
//            }
            return root;
        }

        //delete  node current
        //删除目标根节点（要删除的节点），如果目标根节点的左，右子树都不为null時，根据BSF的特性
        // 1. 将目标节点的左子树，放在右子树的左子树的最左边的叶子节点的左孩子位置上
        // 2. 将目标节点的右孩子作为新的根节点返回
        public TreeNode deletOneNode(TreeNode target) {
            if (target == null) {
                return null;
            }
//            if (target.left == null) {
//                return target.right;
//            }
            if (target.right == null) {
                return target.left;
            }
            //左，右节点都不为空
            TreeNode cur = target.right;
            while (cur.left != null) {
                cur = cur.left;
            }
            cur.left = target.left;
            return target.right;
        }
    }
```