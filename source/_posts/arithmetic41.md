---
title: 剑指 Offer 40. 最小的k个数
date: 2021-07-18 23:15:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

输入整数数组 `arr` ，找出其中最小的 `k` 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

## 示例

> 输入：arr = [3,2,1], k = 2
>
> 输出：[1,2] 或者 [2,1]

<!--more-->

## 限制

- `0 <= k <= arr.length <= 10000`
- `0 <= arr[i] <= 10000`

## 思路 

对原数组从小到大排序后取出前 *k* 个数即可。

## 代码

```java
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        int[] vec = new int[k];
        Arrays.sort(arr);
        for (int i = 0; i < k; ++i) {
            vec[i] = arr[i];
        }
        return vec;
    }
}
```

