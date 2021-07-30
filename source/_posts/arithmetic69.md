---
title: 剑指 Offer 66. 构建乘积数组
date: 2021-07-30 11:04:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

给定一个数组 `A[0,1,…,n-1]`，请构建一个数组 `B[0,1,…,n-1]`，其中 `B[i]` 的值是数组 `A` 中除了下标 `i` 以外的元素的积, 即 `B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]`。不能使用除法。

## 示例

> 输入：[1,2,3,4,5]
> 
>输出： [120,60,40,30,24]

<!--more-->

## 限制

- 所有元素乘积之和不会溢出 32 位整数
- `a.length <= 100000`思路 

## 思路

1. 初始化：数组 B ，其中 B[0] = 1 ；辅助变量 tmp = 1 ；
2. 计算 B[i] 的 下三角 各元素的乘积，直接乘入 B[i] ；
3. 计算 B[i] 的 上三角 各元素的乘积，记为 tmp ，并乘入 B[i] ；
4. 返回 B 。![](arithmetic69/Picture1.PNG)

## 代码

```java
class Solution {
    public int[] constructArr(int[] a) {
        int len = a.length;
        if(len == 0) return new int[0];
        int[] b = new int[len];
        b[0] = 1;
        int tmp = 1;
        for(int i = 1; i < len; i++) {    // 先算下三角
            b[i] = b[i - 1] * a[i - 1];
        }
        for(int i = len - 2; i >= 0; i--) { // 再算上三角
            tmp *= a[i + 1];
            b[i] *= tmp;
        }
        return b;
    }
}
```

