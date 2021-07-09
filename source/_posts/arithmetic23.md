---
title: 剑指 Offer 03. 数组中重复的数字
date: 2021-07-09 22:19:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

## 示例

> 输入：[2, 3, 1, 0, 2, 5, 3]
>
> 输出：2 或 3 
>

<!--more-->

## 限制

- 2 <= n <= 100000

## 思路 

利用数据结构特点，容易想到使用哈希表（Set）记录数组的各个数字，当查找到重复数字则直接返回。

**算法流程：**

1. 初始化： 新建 HashSet ，记为 dic ；
2. 遍历数组 nums 中的每个数字 num ：
   1. 当 num 在 dic 中，说明重复，直接返回 num ；
   2. 将 num 添加至 dic 中；
3. 返回 -1 。本题中一定有重复数字，因此这里返回多少都可以。

## 代码

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        Set<Integer> dic = new HashSet<>();
        for(int num : nums) {
            if(dic.contains(num)) return num;
            dic.add(num);
        }
        return -1;
    }
}
```



