---
title: 剑指 Offer 16. 数值的整数次方
date: 2021-07-07 23:09:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

实现 [pow(*x*, *n*)](https://www.cplusplus.com/reference/valarray/pow/) ，即计算 x 的 n 次幂函数（即，x<sup>n</sup>）。不得使用库函数，同时不需要考虑大数问题。

## 示例

> 输入：x = 2.00000, n = 10
>
> 输出：1024.00000

<!--more-->

> 输入：x = 2.00000, n = -2
>
> 输出：0.25000

## 限制

- -100.0 < x < 100.0
- -2<sup>31</sup> <= n <= 2<sup>31</sup>-1
- -10<sup>4</sup> <= x<sup>n</sup> <= 10<sup>4</sup>

## 思路 

1. 当 x = 0 时：直接返回 0 （避免后续 x = 1 / x 操作报错）。
2. 初始化 res = 1 ；
3. 当 n < 0 时：把问题转化至 n≥0 的范围内，即执行 x = 1/x ，n = - n ；
4. 循环计算：当 n = 0 时跳出；
   1. 当 n \& 1 = 1 时：将当前 x 乘入 res （即 res∗=x ）；
   2. 执行 x = x^2（即 x∗=x ）；
   3. 执行 n 右移一位（即 n >>= 1）。

5. 返回 res 。

## 代码

```java
class Solution {
    public double myPow(double x, int n) {
        if(x == 0) return 0;
        long b = n;
        double res = 1.0;
        if(b < 0) {
            x = 1 / x;
            b = -b;
        }
        while(b > 0) {
            if((b & 1) == 1) res *= x;
            x *= x;
            b >>= 1;
        }
        return res;
    }
}
```



