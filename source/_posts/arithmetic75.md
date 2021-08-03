---
title: 剑指 Offer 63. 股票的最大利润
date: 2021-08-03 23:57:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？

## 示例

> 输入：[7,1,5,3,6,4]
>
> 输出： 5
>
> 解释：在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
>      注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。

<!--more-->

## 限制

- 0 <= 数组长度 <= 10^5

## 思路

1. 状态定义： 设动态规划列表 dp ，dp[i] 代表以 prices[i] 为结尾的子数组的最大利润（以下简称为 前 i 日的最大利润 ）。
2. 转移方程： 由于题目限定 “买卖该股票一次” ，因此前 i 日最大利润 dp[i] 等于前 i−1 日最大利润 dp[i-1] 和第 i 日卖出的最大利润中的最大值。
                                 前i日最大利润 = max(前(i−1)日最大利润,第i日价格−前i日最低价格)
                                                dp[i] =max(dp[i−1],prices[i]−min(prices[0:i]))

3. 初始状态： dp[0] = 0，即首日利润为 00 ；
4. 返回值： dp[n - 1]，其中 n 为 dp 列表长度。

## 代码

```java
class Solution {
    public int maxProfit(int[] prices) {
        int cost = Integer.MAX_VALUE, profit = 0;
        for(int price : prices) {
            cost = Math.min(cost, price);
            profit = Math.max(profit, price - cost);
        }
        return profit;
    }
}
```

