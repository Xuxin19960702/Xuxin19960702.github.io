---
title: 剑指 Offer 55 - I. 二叉树的深度
date: 2020-09-22 16:44:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。





## 示例

给定二叉树 [3,9,20,null,null,15,7]，

　　　　　　　３

　　　　　　/　　\

  　　　　　９　　　２０

　　　　　　　　　/　　\

　　　　　　　　１５　　７

返回它的最大深度 3 。

<!--more-->

## 限制

- 节点总数 <= 10000



## 思路

### 深度优先搜索(DFS)

**算法解析：**

1. **终止条件：** 当 root 为空，说明已越过叶节点，因此返回 深度 0 。

2. **递推工作：** 本质上是对树做后序遍历。

   1. 计算节点 root 的 左子树的深度 ，即调用 maxDepth(root.left)；
   2. 计算节点 root 的 右子树的深度 ，即调用 maxDepth(root.right)；

3. **返回值：** 返回 此树的深度 ，即 max(maxDepth(root.left), maxDepth(root.right)) + 1。

   

### 广度优先搜索(BFS)

**算法解析：**

1. 特例处理： 当 root 为空，直接返回 深度 0 。
2. 初始化： 队列 queue （加入根节点 root ），计数器 res = 0。
3. 循环遍历： 当 queue 为空时跳出。
   1. 初始化一个空列表 tmp ，用于临时存储下一层节点；
   2. 遍历队列： 遍历 queue 中的各节点 node ，并将其左子节点和右子节点加入 tmp；
   3. 更新队列： 执行 queue = tmp ，将下一层节点赋值给 queue；
   4. 统计层数： 执行 res += 1 ，代表层数加 1；
4. 返回值： 返回 res 即可



## 代码

### 深度优先搜索(DFS)

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
    public int maxDepth(TreeNode root) {
        if(root == null) return 0;
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```



### 广度优先搜索(BFS)

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
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        int res = 0;
        while (!queue.isEmpty()) {
            res++;
            int n = queue.size();
            for (int i = 0; i < n; i++) {
                TreeNode node = queue.poll();
                if (node.left != null) queue.add(node.left);
                if (node.right != null) queue.add(node.right);
            }
        }
        return res;
    }
}
```

