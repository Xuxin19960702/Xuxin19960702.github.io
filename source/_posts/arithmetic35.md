---
title: 剑指 Offer 32 - I. 从上到下打印二叉树
date: 2021-07-16 20:39:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

## 示例

> 输入：给定二叉树: `[3,9,20,null,null,15,7]`
>
> 输出：[3,9,20,15,7]

<!--more-->

## 限制

- `节点总数 <= 1000`

## 思路 

1. **特例处理：** 当树的根节点为空，则直接返回空列表 [] ；
2. **初始化：** 打印结果列表 res = [] ，包含根节点的队列 queue = [root] ；
3. **BFS 循环：** 当队列 queue 为空时跳出；
   - **出队：** 队首元素出队，记为 node；
   - **打印：** 将 node.val 添加至列表 tmp 尾部；
   - **添加子节点：** 若 node 的左（右）子节点不为空，则将左（右）子节点加入队列 queue ；
4. **返回值：** 返回打印结果列表 res 即可。

## 代码

```java
class Solution {
    public int[] levelOrder(TreeNode root) {
        if(root == null) return new int[0];
        Queue<TreeNode> queue = new LinkedList<>(){{ add(root); }};
        ArrayList<Integer> ans = new ArrayList<>();
        while(!queue.isEmpty()) {
            TreeNode node = queue.poll();
            ans.add(node.val);
            if(node.left != null) queue.add(node.left);
            if(node.right != null) queue.add(node.right);
        }
        int[] res = new int[ans.size()];
        for(int i = 0; i < ans.size(); i++)
            res[i] = ans.get(i);
        return res;
    }
}
```



