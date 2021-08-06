---
title: 连续数列
date: 2021-08-06 15:48:00
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

给定一个整数数组，找出总和最大的连续数列，并返回总和。

## 示例

> 输入：[-2,1,-3,4,-1,2,1,-5,4]
>
> 输出： 6
>
> 解释：连续子数组 [4,-1,2,1] 的和最大，为 6。

<!--more-->

## 限制

- 如果你已经实现复杂度为 O(*n*) 的解法，尝试使用更为精妙的分治法求解。

## 思路

**贪心：**

- nums[0]存储的是最大值
- nums[i]存储的是当前有效子数列的总和
- 当nums[i-1]小于0时,子数列头部从nums[i]开始算起,然后根据nums[i]的值更新最大值nums[0]

## 代码

```java
// 动态规划
class Solution {
    public int maxSubArray(int[] nums) {
        int pre = 0, maxAns = nums[0];
        for (int x : nums) {
            pre = Math.max(pre + x, x);
            maxAns = Math.max(maxAns, pre);
        }
        return maxAns;
    }
}
```



```java
// 贪心
public int maxSubArray(int[] nums) {
        int len = nums.length;
        for(int i = 1; i < len; i++){    
            nums[i] = nums[i-1] < 0 ? nums[i] : nums[i-1] + nums[i];
            nums[0] = nums[i] > nums[0] ? nums[i] : nums[0];        
        }
        return nums[0];
    }
```

