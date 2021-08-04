---
title: 剑指 Offer 68 - II. 二叉树的最近公共祖先
date: 2021-08-04 16:03:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

## 示例

> 输入：root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
>
> 输出： 3
>
> 解释：节点 5 和节点 1 的最近公共祖先是节点 3。

<!--more-->

## 限制

- 所有节点的值都是唯一的。
- p、q 为不同节点且均存在于给定的二叉树中。

## 思路

1. **终止条件：**
   1. 当越过叶节点，则直接返回 null ；
   2. 当 root 等于 p, q ，则直接返回 root ；
2. **递推工作：**
   1. 开启递归左子节点，返回值记为 left ；
   2. 开启递归右子节点，返回值记为 right ；
3. **返回值：** 根据 left 和 right ，可展开为四种情况；
   1. 当 left 和 right **同时为空 ：**说明 root 的左 / 右子树中都不包含 p,q ，返回 null ；
   2. 当 left 和 right **同时不为空 ：**说明 p, q 分列在 root 的 **异侧** （分别在 左 / 右子树），因此 root 为最近公共祖先，返回 root ；
   3. 当 left **为空** ，right **不为空** ：p,q 都不在 root 的左子树中，直接返回 right 。具体可分为两种情况：
      1. p,q 其中一个在 root 的 **右子树** 中，此时 right 指向 p（假设为 p ）；
      2. p,q 两节点都在 root 的 **右子树** 中，此时的 right 指向 **最近公共祖先节点** ；
   4. 当 left **不为空** ， right **为空** ：与情况 3. 同理；

## 代码

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null || root == p || root == q) return root;
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if(left == null && right == null) return null; // 1.
        if(left == null) return right; // 3.
        if(right == null) return left; // 4.
        return root; // 2. if(left != null and right != null)
    }
}
```


