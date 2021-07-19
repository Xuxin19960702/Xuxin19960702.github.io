---
title: 剑指 Offer 42. 连续子数组的最大和
date: 2021-07-19 21:12:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

## 示例

> 输入：nums = [-2,1,-3,4,-1,2,1,-5,4]
>
> 输出：6
>
> 解释：连续子数组 [4,-1,2,1] 的和最大，为 6。

<!--more-->

## 限制

- `1 <= arr.length <= 10^5`
- `-100 <= arr[i] <= 100`

## 思路 

1. **状态定义：** 设动态规划列表 dp ，dp[i] 代表以元素 nums[i] 为结尾的连续子数组最大和。
   - 为何定义最大和 dp[i] 中必须包含元素 nums[i] ：保证 dp[i] 递推到 dp[i+1] 的正确性；如果不包含 nums[i] ，递推时则不满足题目的 **连续子数组** 要求。

2. **转移方程：** 若 dp[i−1]≤0 ，说明 dp[i - 1] 对 dp[i] 产生负贡献，即 dp[i−1]+nums[i] 还不如 nums[i] 本身大。
   - 当 dp[i−1]>0 时：执行 dp[i]=dp[i−1]+nums[i] ；
   - 当 dp[i−1]≤0 时：执行 dp[i]=nums[i] ；

3. **初始状态：** dp[0]=nums[0]，即以 nums[0]] 结尾的连续子数组最大和为 nums[0] 。

4. **返回值：** 返回 dp 列表中的最大值，代表全局最大值。

## 代码

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int res = nums[0];
        for(int i = 1; i < nums.length; i++) {
            nums[i] += Math.max(nums[i - 1], 0);
            res = Math.max(res, nums[i]);
        }
        return res;
    }
}
```

