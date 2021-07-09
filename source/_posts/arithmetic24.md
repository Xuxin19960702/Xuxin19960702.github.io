---
title: 剑指 Offer 11. 旋转数组的最小数字
date: 2021-07-09 22:35:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。 

## 示例

> 输入：[3,4,5,1,2]
>
> 输出：1

<!--more-->

## 限制

- 2 <= n <= 100000

## 思路 

1. 初始化： 声明 i, j 双指针分别指向 nums 数组左右两端；
2. 循环二分： 设 m = (i + j) / 2 为每次二分的中点（ "/" 代表向下取整除法，因此恒有 i≤m<j ），可分为以下三种情况：
   1. 当 nums[m] > nums[j] 时： m 一定在 左排序数组 中，即旋转点 x 一定在 [m + 1, j][m+1,j] 闭区间内，因此执行 i = m + 1；
   2. 当 nums[m] < nums[j] 时： m 一定在 右排序数组 中，即旋转点 x 一定在[i, m][i,m] 闭区间内，因此执行 j = m；
   3. 当 nums[m] = nums[j] 时： 无法判断 m 在哪个排序数组中，即无法判断旋转点 xx 在 [i, m][i,m] 还是 [m + 1, j][m+1,j] 区间中。解决方案： 执行 j=j−1 缩小判断范围，分析见下文。
3. 返回值： 当 i = j 时跳出二分循环，并返回 旋转点的值 nums[i] 即可。

## 代码

```java
class Solution {
    public int minArray(int[] numbers) {
        int i = 0, j = numbers.length - 1;
        while (i < j) {
            int m = (i + j) / 2;
            if (numbers[m] > numbers[j]) i = m + 1;
            else if (numbers[m] < numbers[j]) j = m;
            else {
                int x = i;
                for(int k = i + 1; k < j; k++) {
                    if(numbers[k] < numbers[x]) x = k;
                }
                return numbers[x];
            }
        }
        return numbers[i];
    }
}
```



