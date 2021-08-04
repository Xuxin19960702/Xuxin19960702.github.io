---
title: 剑指 Offer 68 - I. 二叉搜索树的最近公共祖先
date: 2021-08-04 15:53:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

## 示例

> 输入：root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
>
> 输出： 6 
>
> 解释：节点 2 和节点 8 的最近公共祖先是 6。

<!--more-->

## 限制

- 所有节点的值都是唯一的。
- p、q 为不同节点且均存在于给定的二叉搜索树中。

## 思路

**方法一：迭代**

1. **循环搜索：** 当节点 root 为空时跳出；
   1. 当 p, q 都在 root 的 右子树 中，则遍历至 root.right ；
   2. 否则，当 p, q 都在 root 的 左子树 中，则遍历至 rroot.left ；
   3. 否则，说明找到了 最近公共祖先 ，跳出。
2. **返回值：** 最近公共祖先 root 。



**方法二：递归**

1. 递推工作：
   1. 当 p, q 都在 root 的 右子树 中，则开启递归 root.right 并返回；
   2. 否则，当 p, q 都在 root 的 左子树 中，则开启递归 root.left 并返回；
2. 返回值： 最近公共祖先 root 。

## 代码

```java
// 方法一 迭代
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        while(root != null) {
            if(root.val < p.val && root.val < q.val) // p,q 都在 root 的右子树中
                root = root.right; // 遍历至右子节点
            else if(root.val > p.val && root.val > q.val) // p,q 都在 root 的左子树中
                root = root.left; // 遍历至左子节点
            else break;
        }
        return root;
    }
}
```

```java
// 方法二 递归
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root.val < p.val && root.val < q.val)
            return lowestCommonAncestor(root.right, p, q);
        if(root.val > p.val && root.val > q.val)
            return lowestCommonAncestor(root.left, p, q);
        return root;
    }
}
```

