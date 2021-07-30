---
title: 剑指 Offer 61. 扑克牌中的顺子
date: 2021-07-30 11:17:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。

## 示例

> 输入：[1,2,3,4,5]
> 
>输出： True

<!--more-->

## 限制

- 数组长度为 5 
- 数组的数取值为 [0, 13] .

## 思路

1. 先对数组执行排序。
2. 判别重复： 排序数组中的相同元素位置相邻，因此可通过遍历数组，判断 nums[i] = nums[i + 1] 是否成立来判重。
3. 获取最大 / 最小的牌： 排序后，数组末位元素 nums[4] 为最大牌；元素 nums[joker] 为最小牌，其中 joker 为大小王的数量。

## 代码

```java
// 排序 + 遍历
class Solution {
    public boolean isStraight(int[] nums) {
        int joker = 0;
        Arrays.sort(nums); // 数组排序
        for(int i = 0; i < 4; i++) {
            if(nums[i] == 0) joker++; // 统计大小王数量
            else if(nums[i] == nums[i + 1]) return false; // 若有重复，提前返回 false
        }
        return nums[4] - nums[joker] < 5; // 最大牌 - 最小牌 < 5 则可构成顺子
    }
}
```

