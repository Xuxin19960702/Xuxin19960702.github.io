---
title: 剑指 Offer 32 - II. 从上到下打印二叉树 II
date: 2021-07-16 20:51:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

## 示例

> 输入：给定二叉树: `[3,9,20,null,null,15,7]`
>
> 输出：
>
> [
>   [3],
>   [9,20],
>   [15,7]
> ]

<!--more-->

## 限制

- `节点总数 <= 1000`

## 思路 

1. **特例处理：** 当根节点为空，则返回空列表 [] ；
2. **初始化：** 打印结果列表 res = [] ，包含根节点的队列 queue = [root] ；
3. **BFS 循环：** 当队列 queue 为空时跳出；
   1. 新建一个临时列表 tmp ，用于存储当前层打印结果；
   2. **当前层打印循环：** 循环次数为当前层节点数（即队列 queue 长度）；
      1. 出队： 队首元素出队，记为 node；
      2. 打印： 将 node.val 添加至 tmp 尾部；
      3. 添加子节点： 若 node 的左（右）子节点不为空，则将左（右）子节点加入队列 queue ；
   3. 将当前层结果 tmp 添加入 res 。
4. **返回值：** 返回打印结果列表 res 即可。

## 代码

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> res = new ArrayList<>();
        if(root != null) queue.add(root);
        while(!queue.isEmpty()) {
            List<Integer> tmp = new ArrayList<>();
            for(int i = queue.size(); i > 0; i--) {
                TreeNode node = queue.poll();
                tmp.add(node.val);
                if(node.left != null) queue.add(node.left);
                if(node.right != null) queue.add(node.right);
            }
            res.add(tmp);
        }
        return res;
    }
}
```



