---
title: 剑指 Offer 62. 圆圈中最后剩下的数字
date: 2021-08-03 23:02:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

0,1,···,n-1这n个数字排成一个圆圈，从数字0开始，每次从这个圆圈里删除第m个数字（删除后从下一个数字开始计数）。求出这个圆圈里剩下的最后一个数字。

例如，0、1、2、3、4这5个数字组成一个圆圈，从数字0开始每次删除第3个数字，则删除的前4个数字依次是2、0、4、1，因此最后剩下的数字是3。

## 示例

> 输入：n = 5, m = 3
>
> 输出： 3

<!--more-->

## 限制

- `1 <= n <= 10^5`
- `1 <= m <= 10^6`

## 思路

[LeetCode题解]((https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/solution/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-by-lee/) )



## 代码

```java
class Solution {
    public int lastRemaining(int n, int m) {
        int f = 0;
        for (int i = 2; i != n + 1; ++i) {
            f = (m + f) % i;
        }
        return f;
    }
}
```

