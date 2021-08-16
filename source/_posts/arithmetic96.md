---
title: 两数之和
date: 2021-08-16 17:03:00
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 **和为目标值** target  的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

## 示例

> 输入：nums = [2,7,11,15], target = 9
>
> 输出：[0,1]
>
> 解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。

<!--more-->

## 限制

- `2 <= nums.length <= 104`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`
- **只会存在一个有效答案**

## 思路

使用哈希表，可以将寻找 `target - x` 的时间复杂度降低到从 O*(*N*) 降低到  O*(1)。

## 代码

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> hashtable = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; ++i) {
            if (hashtable.containsKey(target - nums[i])) {
                return new int[]{hashtable.get(target - nums[i]), i};
            }
            hashtable.put(nums[i], i);
        }
        return new int[0];
    }
}
```



