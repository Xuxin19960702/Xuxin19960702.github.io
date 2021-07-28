---
title: 剑指 Offer 53 - I. 在排序数组中查找数字 I
date: 2021-07-27 23:30:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

统计一个数字在排序数组中出现的次数。

## 示例

> 输入：nums = [5,7,7,8,8,10], target = 8
>
> 输出：2

<!--more-->

## 限制

- 0 <= nums.length <= 105
- -109 <= nums[i] <= 109
- nums 是一个非递减数组
- -109 <= target <= 109

## 思路 

1. 初始化： 左边界 i = 0 ，右边界 j = len(nums) - 1 。
2. 循环二分： 当闭区间 [i, j][i,j] 无元素时跳出；
   1. 计算中点 m = (i + j) / 2 （向下取整）；
   2. 若 nums[m] < target ，则 target 在闭区间 [m + 1, j][m+1,j] 中，因此执行 i = m + 1；
   3. 若 nums[m] > target ，则 target 在闭区间 [i, m - 1][i,m−1] 中，因此执行 j = m - 1；
   4. 若 nums[m] = target ，则右边界 right 在闭区间 [m+1, j][m+1,j] 中；左边界 left 在闭区间 [i, m-1][i,m−1] 中。因此分为以下两种情况：
      1. 若查找 右边界 right ，则执行 i = m + 1 ；（跳出时 i 指向右边界）
      2. 若查找 左边界 left ，则执行 j = m - 1 ；（跳出时 j 指向左边界）
3. 返回值： 应用两次二分，分别查找 right 和 left ，最终返回 right - left - 1 即可。

## 代码

```java
class Solution {
    public int search(int[] nums, int target) {
        return helper(nums, target) - helper(nums, target - 1);
    }
    int helper(int[] nums, int tar) {
        int i = 0, j = nums.length - 1;
        while(i <= j) {
            int m = (i + j) / 2;
            if(nums[m] <= tar) i = m + 1;
            else j = m - 1;
        }
        return i;
    }
}
```



