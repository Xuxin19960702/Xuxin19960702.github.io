---
title: 剑指 Offer 53 - II. 0～n-1中缺失的数字
date: 2021-07-28 10:45:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

## 示例

> 输入：[0,1,2,3,4,5,6,7,9]
>
> 输出：8

<!--more-->

## 限制

- 1 <= 数组长度 <= 10000

## 思路 

1. 初始化： 左边界 i = 0 ，右边界 j = len(nums) - 1 ；代表闭区间 [i, j][i,j] 。
2. 循环二分： 当 i ≤ j 时循环 （即当闭区间 [i, j][i,j] 为空时跳出） ；
   1. 计算中点 m = (i + j) // 2 ，其中 "//" 为向下取整除法；
   2. 若 nums[m] = m ，则 “右子数组的首位元素” 一定在闭区间 [m + 1, j][m+1,j] 中，因此执行 i = m + 1；
   3. 若 nums[m] ≠ m ，则 “左子数组的末位元素” 一定在闭区间 [i, m - 1][i,m−1] 中，因此执行 j = m - 1；
3. 返回值： 跳出时，变量 i 和 j 分别指向 “右子数组的首位元素” 和 “左子数组的末位元素” 。因此返回 i 即可。

## 代码

```java
class Solution {
    public int missingNumber(int[] nums) {
        int i = 0, j = nums.length - 1;
        while(i <= j) {
            int m = (i + j) / 2;
            if(nums[m] == m) i = m + 1;
            else j = m - 1;
        }
        return i;
    }
}
```



