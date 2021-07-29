---
title: 剑指 Offer 54. 二叉搜索树的第k大节点
date: 2021-07-28 09:41:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

给定一棵二叉搜索树，请找出其中第k大的节点。

## 示例

> 输入：root = [3,1,4,null,2], k = 1
>
> 输出：4

<!--more-->

## 限制

- 1 ≤ k ≤ 二叉搜索树元素个数

## 思路 

1. 终止条件： 当节点 root 为空（越过叶节点），则直接返回；
2. 递归右子树： 即 dfs(root.right) ；
3. 三项工作：
   1. 提前返回： 若 k = 0 ，代表已找到目标节点，无需继续遍历，因此直接返回；
   2. 统计序号： 执行 k = k - 1 （即从 k 减至 0 ）；
   3. 记录结果： 若 k = 0 ，代表当前节点为第 k 大的节点，因此记录 res = root.val ；
4. 递归左子树： 即 dfs(root.left) ；

## 代码

```java
class Solution {
    int res, k;
    public int kthLargest(TreeNode root, int k) {
        this.k = k;
        dfs(root);
        return res;
    }
    void dfs(TreeNode root) {
        if(root == null) return;
        dfs(root.right);
        if(k == 0) return;
        if(--k == 0) res = root.val;
        dfs(root.left);
    }
}


```

