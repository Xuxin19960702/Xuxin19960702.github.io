---
title: 剑指 Offer II 010. 和为 k 的子数组
date: 2021-08-10 15:28:00
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

给定一个整数数组和一个整数 `k` **，**请找到该数组中和为 `k` 的连续子数组的个数。

## 示例

> 输入：nums = [1,1,1], k = 2
>
> 输出：2
>
> 解释：此题 [1,1] 与 [1,1] 为两种不同的情况

<!--more-->

## 限制

- `1 <= nums.length <= 2 * 104`
- `-1000 <= nums[i] <= 1000`
- `-107 <= k <= 107`

## 思路

1.静态区间和---->前缀和

2.哈希字典加速查找

## 代码

```java
class Solution 
{
    public int subarraySum(int[] nums, int k) 
    {
        Map<Integer, Integer> presum_cnt = new HashMap<>();
        presum_cnt.put(0, 1);

        int res = 0;
        int pre = 0;
        for (int y : nums)
        {
            pre += y;
            int x = pre - k;
            res += presum_cnt.getOrDefault(x, 0);
            presum_cnt.put(pre, presum_cnt.getOrDefault(pre, 0) + 1);
        }

        return res;
    }
}
```



