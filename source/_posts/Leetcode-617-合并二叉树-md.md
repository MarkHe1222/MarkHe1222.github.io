---
title: Leetcode-617-合并二叉树
date: 2020-04-21 21:21:15
categories: Algorithm
tags: Leetcode

---

## 617. 合并二叉树

**题目：**

```
给定两个二叉树，想象当你将它们中的一个覆盖到另一个上时，两个二叉树的一些节点便会重叠。

你需要将他们合并为一个新的二叉树。合并的规则是如果两个节点重叠，那么将他们的值相加作为节点合并后的新值，否则**不为** NULL 的节点将直接作为新二叉树的节点。 
```

**示例：**

```输入: 
	Tree 1                     Tree 2                  
          1                         2                             
         / \                       / \                            
        3   2                     1   3                        
       /                           \   \                      
      5                             4   7                  
输出: 
合并后的树:
	     3
	    / \
	   4   5
	  / \   \ 
	 5   4   7
	 
注意: 合并必须从两个树的根节点开始。
```

**思路：**

涉及二叉树相关的算法，首先要考虑到递归调用（二叉树遍历常用套路）

因为这里需要重新生成一棵新的数，我们只要选取其中的一棵树为基准就行，如另外一棵树的节点为null的话，则返回另一棵树的节点。以此遍历所有的节点，最后返回新树的根节点。

**代码：**

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if (t1 == null && t2 == null) {
            return null;
        }
        if (t1 == null) {
            return t2;
        }
        if (t2 == null) {
            return t1;
        }

        t1.val = t1.val + t2.val;
        t1.left = mergeTrees(t1.left, t2.left);
        t1.right = mergeTrees(t1.right, t2.right);
        return t1;
    }
}
```

