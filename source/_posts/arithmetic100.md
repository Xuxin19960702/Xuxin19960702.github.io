---
title: 整数反转
date: 2021-08-18 19:54:00
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

给你一个 32 位的有符号整数 x ，返回将 x 中的数字部分反转后的结果。

如果反转后整数超过 32 位的有符号整数的范围 [−2<sup>31</sup>,  2<sup>31</sup> − 1] ，就返回 0。

**假设环境不允许存储 64 位整数（有符号或无符号）。**

## 示例

> 输入：x = 123
>    
>输出：321
> 

<!--more-->

## 限制

- -2<sup>31</sup> <= x <= 2<sup>31</sup> - 1

## 思路

越界前提前判断

## 代码

```java
class Solution {
    public int reverse(int x) {
        int rev = 0;
        while (x != 0) {
            if (rev < Integer.MIN_VALUE / 10 || rev > Integer.MAX_VALUE / 10) {
                return 0;
            }
            int digit = x % 10;
            x /= 10;
            rev = rev * 10 + digit;
        }
        return rev;
    }
}
```

