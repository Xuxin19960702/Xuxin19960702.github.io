---
title: 剑指 Offer 27. 二叉树的镜像
date: 2020-09-22 15:25:33
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

请完成一个函数，输入一个二叉树，该函数输出它的镜像。



例如输入：           　　　　　　                       镜像输出：

 　   4                           　　　　　　　　　　                   4

  　 /　\                     　　　 　　　　　　                      /  　 \
 　2　   7                   　　　　　　　　　                    7　 　2
   /　\    / 　\                      　　　　     　　　             / 　\    /　  \
1　3     6　9                     　　　 　　　                 9　　6 3　　1



<!--more-->

## **示例 1**

> 输入：root = [4,2,7,1,3,6,9]
> 输出：[4,7,2,9,6,3,1]



## **限制**

- 0 <= 节点个数 <= 1000



## 思路

根据二叉树镜像的定义，考虑递归遍历（DFS）换每个节点的左 / 右子节点，即可生成二叉树的镜像。

1. **递归解析：**
   终止条件： 当节点 `root` 为空时（即越过叶节点），则返回 `null` 
2. **递推工作：**
   1. 初始化节点 `tmp`，用于暂存 `root` 的左子节点
   2. 开启递归 右子节点 `mirrorTree``(root.right)`，并将返回值作为 `root` 的 **左子节点** 
   3. 开启递归 左子节点 `mirrorTree(tmp)` ，并将返回值作为 `root` 的 **右子节点** 。
3. **返回值：** 返回当前节点 `root`



## 代码

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
    public TreeNode mirrorTree(TreeNode root) {
        if(root == null) return null;
        TreeNode tmp = root.left;
        root.left = mirrorTree(root.right);
        root.right = mirrorTree(tmp);
        return root;
    }
}
```

