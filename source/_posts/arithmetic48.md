---
title: 剑指 Offer 33. 二叉搜索树的后序遍历序列
date: 2021-07-20 20:38:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 `true`，否则返回 `false`。假设输入的数组的任意两个数字都互不相同。

## 示例

> 输入：[1,6,3,2,5]
>
> 输出：false

<!--more-->

## 限制

- `数组长度 <= 1000`

## 思路 

1. **初始化：** 单调栈 stack ，父节点值 root=+∞ （初始值为正无穷大，可把树的根节点看为此无穷大节点的左孩子）；
2. **倒序遍历** postorder ：记每个节点为 r<sub>i</sub>；
   - **判断：** 若 r<sub>i</sub> > root，说明此后序遍历序列不满足二叉搜索树定义，直接返回 false；
   - **更新父节点 root ：** 当栈不为空 且r<sub>i</sub> < stack.peek() 时，循环执行出栈，并将出栈节点赋给 root。
   - **入栈：** 将当前节点r<sub>i</sub>入栈；

3. 若遍历完成，则说明后序遍历满足二叉搜索树定义，返回 true 。

## 代码

```java
class Solution {
    public boolean verifyPostorder(int[] postorder) {
        Stack<Integer> stack = new Stack<>();
        int root = Integer.MAX_VALUE;
        for(int i = postorder.length - 1; i >= 0; i--) {
            if(postorder[i] > root) return false;
            while(!stack.isEmpty() && stack.peek() > postorder[i])
            	root = stack.pop();
            stack.add(postorder[i]);
        }
        return true;
    }
}
```

