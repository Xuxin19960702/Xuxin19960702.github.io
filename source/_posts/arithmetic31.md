---
title: 剑指 Offer 28. 对称的二叉树
date: 2021-07-14 21:57:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

## 示例

> 输入：root = [1,2,2,3,4,4,3]
>
> 输出：true

<!--more-->

## 限制

- 0 <= 节点个数 <= 10000

## 思路 

**`isSymmetric(root) ：`**

- 特例处理： 若根节点 root 为空，则直接返回 true 。
- 返回值： 即 recur(root.left, root.right) ;

**`recur(L, R)` ：**

- 终止条件：
  - 当 L 和 R 同时越过叶节点： 此树从顶至底的节点都对称，因此返回 true ；
  - 当 L 或 R 中只有一个越过叶节点： 此树不对称，因此返回 false ；
  - 当节点 L 值  ≠ 节点 R 值： 此树不对称，因此返回 false ；
- 递推工作：
  - 判断两节点 L.leftL 和 R.rightR 是否对称，即 recur(L.left, R.right) ；
  - 判断两节点 L.rightL 和 R.leftR 是否对称，即 recur(L.right, R.left) ；
  - 返回值： 两对节点都对称时，才是对称树，因此用与逻辑符 `&&` 连接。



## 代码

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return root == null ? true : recur(root.left, root.right);
    }
    boolean recur(TreeNode L, TreeNode R) {
        if(L == null && R == null) return true;
        if(L == null || R == null || L.val != R.val) return false;
        return recur(L.left, R.right) && recur(L.right, R.left);
    }
}

```



