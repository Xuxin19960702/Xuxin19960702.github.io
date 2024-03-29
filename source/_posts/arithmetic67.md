---
title: 剑指 Offer 65. 不用加减乘除做加法
date: 2021-07-30 10:25:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

## 示例

> 输入：a = 1, b = 1
>
> 输出：2

<!--more-->

## 限制

- `a`, `b` 均可能是负数或 0
- 结果不会溢出 32 位整数

## 思路 

设两数字的二进制形式 *a*,*b* ，其求和 *s*=*a*+*b* ，*a*(*i*) 代表 *a* 的二进制第 *i* 位，则分为以下四种情况：

| *a*(*i*) | *b*(*i*) | **无进位和** *n*(*i*) | **进位** *c*(*i*+1) |
| :------: | :------: | :-------------------: | :-----------------: |
|    0     |    0     |           0           |          0          |
|    0     |    1     |           1           |          0          |
|    1     |    0     |           1           |          0          |
|    1     |    1     |           0           |          1          |

观察发现，**无进位和** 与 **异或运算** 规律相同，**进位** 和 **与运算** 规律相同（并需左移一位）。因此，无进位和 n*n* 与进位 *c* 的计算公式如下；

> *n*=*a*⊕*b*	非进位和：异或运算
>
> *c*=*a*&*b*<<1	进位：与运算+左移一位

（和 s ）=（非进位和 n ）+（进位 c ）。即可将 s = a + b 转化为：
																		s = a + b ⇒ s = n + c

![](arithmetic67/Picture1.Png)

> Q ： 若数字 a 和 b 中有负数，则变成了减法，如何处理？
> A ： 在计算机系统中，数值一律用 补码 来表示和存储。补码的优势： 加法、减法可以统一处理（CPU只有加法器）。因此，以上方法 同时适用于正数和负数的加法 。

## 代码

```java
class Solution {
    public int add(int a, int b) {
        while(b != 0) { // 当进位为 0 时跳出
            int c = (a & b) << 1;  // c = 进位
            a ^= b; // a = 非进位和
            b = c; // b = 进位
        }
        return a;
    }
}
```

