---
title: 剑指 Offer 44. 数字序列中某一位的数字
date: 2021-07-20 20:10:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。

## 示例

> 输入：n = 3
>
> 输出：3

<!--more-->

## 限制

- `0 <= n < 2^31`

## 思路 

> 将 101112⋯ 中的每一位称为 **数位** ，记为 n ；
> 将 10,11,12,⋯ 称为 **数字** ，记为 num ；
> 数字 10 是一个两位数，称此数字的 **位数** 为 2 ，记为 digit；
> 每 digit 位数的起始数字（即：1,10,100,⋯），记为 start 。

![](arithmetic47/Picture1.png)

1. 确定所求数位的所在数字的位数

   `count = 9 × start × digit`

2. 确定所求数位所在的数字num

   `num = start + (n - 1) / digit`

3. 确定所求数位在 num 的哪一数位

   `(n - 1) % digit`

## 代码

```java
class Solution {
    public int findNthDigit(int n) {
        int digit = 1;
        long start = 1;
        long count = 9;
        while (n > count) { // 1.
            n -= count;
            digit += 1;
            start *= 10;
            count = digit * start * 9;
        }
        long num = start + (n - 1) / digit; // 2.
        return Long.toString(num).charAt((n - 1) % digit) - '0'; // 3.
    }
}
```

