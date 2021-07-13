---
title: 剑指 Offer 14- I. 剪绳子
date: 2021-07-13 23:10:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

## 示例

> 输入：10
>
> 输出：36
>
> 解释：10 = 3 + 3 + 4, 3 × 3 × 4 = 36

<!--more-->

## 限制

- 0 <= n <= 58

## 思路 

1. 当 n≤3 时，按照规则应不切分，但由于题目要求必须剪成 m>1 段，因此必须剪出一段长度为 1 的绳子，即返回 n−1 。
2. 当 n>3 时，求 n 除以 3 的 整数部分 a 和 余数部分 b （即 n=3a+b ），并分为以下三种情况：
   - 当 b=0 时，直接返回 3<sup>a</sup>；
   - 当 b=1 时，要将一个 1 + 3 转换为 2+2，因返回 3<sup>a−1</sup>× 4；
   - 当 b=2 时，返回 3<sup>a</sup> × 2。

## 代码

```java
class Solution {
    public int cuttingRope(int n) {
        if(n <= 3) return n - 1;
        int a = n / 3, b = n % 3;
        if(b == 0) return (int)Math.pow(3, a);
        if(b == 1) return (int)Math.pow(3, a - 1) * 4;
        return (int)Math.pow(3, a) * 2;
    }
}

```



