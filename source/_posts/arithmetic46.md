---
title: 剑指 Offer 39. 数组中出现次数超过一半的数字
date: 2021-07-20 19:40:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

## 示例

> 输入：[1, 2, 3, 2, 2, 2, 5, 4, 2]
>
> 输出：2

<!--more-->

## 限制

1 <= 数组长度 <= 50000

## 思路 

1. 初始化： 票数统计 votes = 0 ， 众数 x；
2. 循环： 遍历数组 nums 中的每个数字 num ；
   1. 当 票数 votes 等于 0 ，则假设当前数字 num 是众数；
   2. 当 num = x 时，票数 votes 自增 1 ；当 num != x 时，票数 votes 自减 1 ；
3. 返回值： 返回 x 即可；

## 代码

```java
class Solution {
    public int majorityElement(int[] nums) {
        int x = 0, votes = 0;
        for(int num : nums){
            if(votes == 0) x = num;
            votes += num == x ? 1 : -1;
        }
        return x;
    }
}
```

