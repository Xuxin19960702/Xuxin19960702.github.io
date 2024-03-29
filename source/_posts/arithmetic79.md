---
title: 你能在你最喜欢的那天吃到你最喜欢的糖果吗？
date: 2021-08-05 15:56:00
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

给你一个下标从 **0** 开始的正整数数组 `candiesCount` ，其中 `candiesCount[i]` 表示你拥有的第 i 类糖果的数目。同时给你一个二维数组 `queries` ，其中 `queries[i] = [favoriteTypei, favoriteDayi, dailyCapi]` 。

你按照如下规则进行一场游戏：

- 你从第 **0** 天开始吃糖果。

- 你在吃完 **所有** 第 i - 1 类糖果之前，**不能** 吃任何一颗第 i 类糖果。

- 在吃完所有糖果之前，你必须每天 **至少** 吃 **一颗** 糖果。

  <!--more-->

请你构建一个布尔型数组 `answer` ，用以给出 `queries` 中每一项的对应答案。此数组满足：

- `answer.length == queries.length` 。`answer[i]` 是 `queries[i]` 的答案。
- `answer[i]` 为 `true` 的条件是：在每天吃 **不超过** `dailyCapi` 颗糖果的前提下，你可以在第 `favoriteDayi` 天吃到第 `favoriteTypei` 类糖果；否则 `answer[i]` 为 `false` 。

注意，只要满足上面 3 条规则中的第二条规则，你就可以在同一天吃不同类型的糖果。

请你返回得到的数组 `answer` 。

## 示例

> 输入：candiesCount = [7,4,5,3,8], queries = [[0,2,2],[4,2,4],[2,13,1000000000]]
>
> 输出： [true,false,true]
>
> 解释：
>
> 1- 在第 0 天吃 2 颗糖果(类型 0），第 1 天吃 2 颗糖果（类型 0），第 2 天你可以吃到类型 0 的糖果。
> 2- 每天你最多吃 4 颗糖果。即使第 0 天吃 4 颗糖果（类型 0），第 1 天吃 4 颗糖果（类型 0 和类型 1），你也没办法在第 2 天吃到类型 4 的糖果。换言之，你没法在每天吃 4 颗糖果的限制下在第 2 天吃到第 4 类糖果。
> 3- 如果你每天吃 1 颗糖果，你可以在第 13 天吃到类型 2 的糖果。

## 限制

- m == matrix.length
- n == matrix[i].length
- 1 <= m, n <= 200
- 0 <= matrix[i][j] <= 231 - 1

## 思路

对于第 i 个询问 (*favoriteType<sub>i</sub> ,favoriteDay<sub>i</sub>,dailyCap<sub>i</sub>*)，我们每天至少吃 1 颗糖果，至多吃 dailyCap<sub>i</sub>颗糖果，因此我们吃的糖果的数量落在区间：

​                                           [*favoriteDay<sub>i</sub>* + 1, (*favoriteDay<sub>i</sub>* + 1) × *dailyCap<sub>i</sub>*]

内。那么只要这个区间包含了一颗第 *favoriteType<sub>i</sub>* 种类型的糖果，就可以满足要求了。

因此我们求出糖果数量的前缀和，记录在数组 *sum* 中，那么第 *favoriteType<sub>i</sub>* 种类型的糖果对应的编号范围为：

​                                           [ *sum*[*favoriteType<sub>i</sub>* − 1] + 1, *sum*[*favoriteType<sub>i</sub>*] ]

特别地，如果 *favoriteType<sub>i</sub>* 为 0，那么区间的左端点为 1。

我们只要判断这两个区间是否有交集即可。如果有交集，说明我们可以吃到第 favoriteType<sub>i</sub>类的糖果。判断是否有交集的方法如下：

> 对于区间 [x<sub>i</sub>, y<sub>i</sub>][x 1 ,y 1 ] 以及 [x<sub>i</sub>, y<sub>i</sub>][x 2 ,y 2 ]，它们没有交集当且仅当 x<sub>1</sub> > y<sub>2</sub> 或者 y<sub>1</sub> < x<sub>2</sub>

## 代码

```java
class Solution {
    public boolean[] canEat(int[] candiesCount, int[][] queries) {
        int n = candiesCount.length;
        
        // 前缀和
        long[] sum = new long[n];
        sum[0] = candiesCount[0];
        for (int i = 1; i < n; ++i) {
            sum[i] = sum[i - 1] + candiesCount[i];
        }
        
        int q = queries.length;
        boolean[] ans = new boolean[q];
        for (int i = 0; i < q; ++i) {
            int[] query = queries[i];
            int favoriteType = query[0], favoriteDay = query[1], dailyCap = query[2];
            
            long x1 = favoriteDay + 1;
            long y1 = (long) (favoriteDay + 1) * dailyCap;
            long x2 = favoriteType == 0 ? 1 : sum[favoriteType - 1] + 1;
            long y2 = sum[favoriteType];
            
            ans[i] = !(x1 > y2 || y1 < x2);
        }
        return ans;
    }
}
```



