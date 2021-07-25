---
title: 剑指 Offer 57. 和为s的两个数字
date: 2021-07-24 23:29:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

## 示例

> 输入：nums = [2,7,11,15], target = 9
>
>    输出：[2,7] 或者 [7,2]

<!--more-->

## 限制

- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^6`

## 思路 

1. **初始化：** 双指针 i , j 分别指向数组 nums 的左右两端 （俗称对撞双指针）。
2. **循环搜索：** 当双指针相遇时跳出；
   1. 计算和 s = nums[i] + nums[j]；
   2. 若 s > target ，则指针 j 向左移动，即执行 j = j - 1；
   3. 若 s < target ，则指针 i 向右移动，即执行 i = i + 1；
   4. 若 s = target ，立即返回数组 [nums[i], nums[j]]；
3. 返回空数组，代表无和为 target 的数字组合。



## 代码

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int i = 0, j = nums.length - 1;
        while(i < j) {
            int s = nums[i] + nums[j];
            if(s < target) i++;
            else if(s > target) j--;
            else return new int[] { nums[i], nums[j] };
        }
        return new int[0];
    }
}

```



