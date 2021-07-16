---
title: 合并区间
date: 2021-07-16 21:45:00
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

以数组 intervals 表示若干个区间的集合，其中单个区间为 intervals[i] = [starti, endi] 。请你合并所有重叠的区间，并返回一个不重叠的区间数组，该数组需恰好覆盖输入中的所有区间。

## 示例

> 输入：intervals = [[1,3],[2,6],[8,10],[15,18]]
>
> 输出：[[1,6],[8,10],[15,18]]
>
> 解释：区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6]

<!--more-->

## 限制

- 1 <= intervals.length <= 104
- intervals[i].length == 2
- 0 <= starti <= endi <= 104

## 思路 

1. 对起点和终点分别进行排序，将起点和终点一一对应形成一个数组。
   - 如果没有overlap,返回当前起点和终点
   - 如果有overlap,判断以下条件

2. 找出最小的起点
3. 如果当前终点大于下一个数组的起点的时候，比较当前终点和下一个终点的大小，取为right
4. 返回满足要求的区间[[left,right]]

## 代码

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        List<int[]> res = new ArrayList<>();
        if (intervals.length == 0 || intervals == null) return res.toArray(new int[0][2]);
        // 对起点终点进行排序
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        int i = 0;
        while (i < intervals.length) {
            int left = intervals[i][0];
            int right = intervals[i][1];
            // 如果有重叠，循环判断哪个起点满足条件
            while (i < intervals.length - 1 && intervals[i + 1][0] <= right) {
                i++;
                right = Math.max(right, intervals[i][1]);
            }
            // 将现在的区间放进res里面
            res.add(new int[]{left, right});
            // 接着判断下一个区间
            i++;
        }
        return res.toArray(new int[0][]);
    }
}
```



