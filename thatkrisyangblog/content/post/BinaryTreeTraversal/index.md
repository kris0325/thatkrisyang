---
title: Binary Tree Traversal
description: 二叉樹的遍歷
slug: 二叉樹的遍歷的遞歸實現與迭代實現
date: 2024-07-07
image: BinaryTreeTraversal.png
categories:
  - leetcode
tags:
  - Binary Tree
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---
## 二叉樹的遍歷，常規遞歸與迭代實現
**二叉樹前序遍歷**

[144.binary-tree-preorder-traversal.java](https://kris0325.github.io/p/144.binary-tree-preorder-traversal.java/)

**二叉樹中序遍歷**

[94.binary-tree-inorder-traversal.java](https://kris0325.github.io/p/94.binary-tree-inorder-traversal.java/)

**二叉樹後序遍歷**

[145.binary-tree-postorder-traversal.java](https://kris0325.github.io/p/145.binary-tree-postorder-traversal.java/)



### 二叉樹前序遍歷

[144.binary-tree-preorder-traversal.java](https://kris0325.github.io/p/144.binary-tree-preorder-traversal.java/)

```java

/*
 * 思路：遞歸實現
 * 中-左-右
 */
class Solution1 {
    List<Integer> result = new ArrayList<>();

    public List<Integer> preorderTraversal(TreeNode root) {
        if (null == root) {
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

### 二叉樹中序遍歷

[94.binary-tree-inorder-traversal.java](https://kris0325.github.io/p/94.binary-tree-inorder-traversal.java/)

```java
 /*
 * 思路：遞歸實現中序遍歷
 * 左-右-中
 *
 * */
class Solution1 {
    List<Integer> result = new ArrayList<>();

    public List<Integer> inorderTraversal(TreeNode root) {

        if (null == root) {

            return result;
        }
        if (root.left != null) {
            inorderTraversal(root.left);
        }
        result.add(root.val);
        if (root.right != null) {
            inorderTraversal(root.right);
        }
        return result;
    }

}

/*
 * 思路：迭代實現中序遍歷
 *
 *
 * */
class Solution {
    List<Integer> result = new ArrayList<>();

    public List<Integer> inorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        while (cur != null || !stack.isEmpty()) {
            //左
            while (cur != null) {
                stack.push(cur);
                cur = cur.left;
            }
            //中
            cur = stack.pop();
            result.add(cur.val);
            //右
            cur = cur.right;
        }
        return result;
    }

}
```

### 二叉樹後序遍歷

[145.binary-tree-postorder-traversal.java](https://kris0325.github.io/p/145.binary-tree-postorder-traversal.java/)

```java
/*
 * 思路1：递归实现后序遍历
 * 左-右-中
 */
class Solution1 {
    List<Integer> result = new ArrayList<>();

    public List<Integer> postorderTraversal(TreeNode root) {
        if (null == root) {
            return result;
        }
        postorderTraversal(root.left);
        postorderTraversal(root.right);
        result.add(root.val);
        return result;
    }
}

/*
 * 思路2：stack递归实现后序遍历，使用一个额外的栈反转节点
 */
class Solution2 {
    List<Integer> result = new ArrayList<>();

    public List<Integer> postorderTraversal(TreeNode root) {
        if (root == null) {
            return result;
        }
        Stack<TreeNode> stack1 = new Stack<>();
        Stack<TreeNode> stack2 = new Stack<>();
        stack1.push(root);
        while (!stack1.isEmpty()) {
            TreeNode node = stack1.pop();
            stack2.push(node);
            if (node.left != null) {
                stack1.push(node.left);
            }
            if (node.right != null) {
                stack1.push(node.right);
            }
        }
        while (!stack2.isEmpty()) {
            result.add(stack2.pop().val);
        }
        return result;
    }
}


/*
 * 思路3：stack递归实现后序遍历，借鉴前序遍历的遞歸遍歷，稍微调整下入栈顺序即可
 * 前序遍歷是：中-左-右，後序遍歷是左-右-中，那麼調整前序遍歷的代碼順序，變成中-右-左，
 * 然後再反轉result數組，即可得到後序遍歷的順序
 */
class Solution {
    List<Integer> result = new ArrayList<>();

    public List<Integer> postorderTraversal(TreeNode root) {
        if (root == null) {
            return result;
        }
        Stack<Integer> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            result.add(node.val);
            if (root.left != null) {
                stack.push(root.left);
            }
            if (root.right != null) {
                stack.push(root.left);
            }
        }
        result.reversed();
        return result;
    }
}
```

此时我们用迭代法写出了二叉树的前后中序遍历，大家可以看出前序和中序是完全两种代码风格，并不像递归写法那样代码稍做调整，就可以实现前后中序。
**这是因为前序遍历中访问节点（遍历节点）和处理节点（将元素放进result数组中）可以同步处理，但是中序就无法做到同步！**

## 二叉樹的迭代遍歷統一寫法

> 在二叉树：听说递归能做的，栈也能做！
> 中提到说使用栈的话，无法同时解决访问节点（遍历节点）和处理节点（将元素放进结果集）不一致的情况。

> 那我们就将访问的节点放入栈中，把要处理的节点也放入栈中但是要做标记。

>如何标记呢，就是要处理的节点放入栈之后，紧接着放入一个空指针作为标记。 这种方法也可以叫做标记法。

#

### 前序遍歷的遞歸實現
```java
/*
 * 前序遍歷 中-左-右，基於標記法遞歸實現
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
            TreeNode node = stack.peek();
            if (null != node) {
                stack.pop();
                //右
                if (null != node.right) {
                    stack.push(node.right);
                }
                //左
                if (null != node.left) {
                    stack.push(node.left);
                }
                //中
                stack.push(node);
                //中節點訪問過，但還沒處理，加入null節點標記。標記上一個節點是需要處理的節點
                stack.push(null);
            } else {
                //當判斷pop()的節點為null ,則先pop,再取第二個節點便是為需要處理節點
                stack.pop();
                result.add(stack.pop().val);
            }
        }
        return result;
    }
}
```


### 中序遍歷的遞歸實現

```java
/*
 * 中序遍歷 左-中-右，基於標記法遞歸實現
 */
class Solution {
    List<Integer> result = new ArrayList<>();
    public List<Integer> inorderTraversal(TreeNode root) {
        if (null == root) {
            return result;
        }
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.peek();
            if (null != node) {
                stack.pop();
                //右
                if (null != node.right) {
                    stack.push(node.right);
                }
                //中
                stack.push(node);
                //中節點訪問過，但還沒處理，加入null節點標記。標記上一個節點是需要處理的節點
                stack.push(null);
                //左
                if (null != node.left) {
                    stack.push(node.left);
                }
    
            } else {
                //當判斷pop()的節點為null ,則先pop,再取第二個節點便是為需要處理節點
                stack.pop();
                result.add(stack.pop().val);
            }
        }
        return result;
    }
}

```

### 後序遍歷的遞歸實現

```java
/*
 * 後序遍歷 左-右-右，基於標記法遞歸實現
 */
class Solution {
    List<Integer> result = new ArrayList<>();
    public List<Integer> postorderTraversal(TreeNode root) {
        if (null == root) {
            return result;
        }
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.peek();
            if (null != node) {
                stack.pop();
                //中
                stack.push(node);
                //中節點訪問過，但還沒處理，加入null節點標記。標記上一個節點是需要處理的節點
                stack.push(null);
                //右
                if (null != node.right) {
                    stack.push(node.right);
                }
                //左
                if (null != node.left) {
                    stack.push(node.left);
                }
    
            } else {
                //當判斷pop()的節點為null ,則先pop,再取第二個節點便是為需要處理節點
                stack.pop();
                result.add(stack.pop().val);
            }
        }
        return result;
    }
}
```