---
title: Leetcode-199-二叉树的右视图
date: 2020-04-23 01:48:09
categories: Algorithm
tags: Leetcode

---

## 199. 二叉树的右视图

**题目：**

```
给定一棵二叉树，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。
```

**示例：**

```
输入: [1,2,3,null,5,null,4]
输出: [1, 3, 4]
解释:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```

**思路：**

思路1（DFS）:

老套路，看到树相关的题目，首先要联想到递归调用，遍历树等关键词。根据题意，我们需要找出树的每一层的最后一个节点。根据前序遍历的顺序 [根节点-> 左节点 -> 右节点] ，可以推断出与其相反的遍历顺序 [根节点 -> 右节点 -> 左节点] ，如此就可以保证每次先访问到右节点，如果右节点为空则再遍历左节点。

**代码：**

```java
public class RightSideView_199 {
    // DFS
    List<Integer> res = new ArrayList<>();

    public List<Integer> rightSideView(TreeNode root) {
        dfs(root, 0);
        return res;
    }

    private void dfs(TreeNode root, int depth) {
        if (root == null) {
            return;
        }
        // 先访问 当前节点，再递归地访问 右子树 和 左子树
      	// 如果当前节点所在深度还没有出现在res里，说明在该深度下当前节点是第一个被访问的节点，因此将当前节点加入res中。
        if (res.size() == depth) {
            res.add(root.val);
        }
        depth++;
        dfs(root.right, depth);
        dfs(root.left, depth);
    }
}
```

思路2（BFS）:

根据广度优先的遍历算法，我们只要记住每一层树的最后一个元素就能满足题意要求了。

**代码：**

```java
public class RightSideView_199 {
    // BFS
    public List<Integer> rightSideView_2(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        // 将每层的所有节点都放在queue中
        Queue<TreeNode> queue = new LinkedList<>();
        // 第一层的根节点
        queue.offer(root);
        // 遍历所有层，直至最后一层
        while (!queue.isEmpty()) {
            int size = queue.size();
            // 遍历每一层的所有节点，并将下一层的所有节点放入queue中
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (node.left != null) {
                    queue.offer(node.left);
                }
                if (node.right != null) {
                    queue.offer(node.right);
                }
                // 将当前层的最后一个节点放入结果列表
                if (i == size - 1) {
                    res.add(node.val);
                }
            }
        }
        return res;
    }
}
```



