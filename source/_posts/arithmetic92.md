---
title: 形成两个异或相等数组的三元组数目
date: 2021-08-14 18:52:00
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

给你一个整数数组 arr 。

现需要从数组中取三个下标 i、j 和 k ，其中 (0 <= i < j <= k < arr.length) 。

a 和 b 定义如下：

a = arr[i] ^ arr[i + 1] ^ ... ^ arr[j - 1]
b = arr[j] ^ arr[j + 1] ^ ... ^ arr[k]
注意：^ 表示 按位异或 操作。

请返回能够令 a == b 成立的三元组 (i, j , k) 的数目。

## 示例

> 输入：arr = [2,3,1,6,7]
>
> 输出：4
>
> 解释：满足题意的三元组分别是 (0,1,2), (0,2,2), (2,3,4) 以及 (2,4,4)

<!--more-->

## 限制

- `1 <= arr.length <= 300`
- `1 <= arr[i] <= 10^8`

## 思路

S<sub>i</sub> ⊕ S<sub>j</sub> = (arr<sub>0</sub> ⊕ arr<sub>1</sub> ⊕⋯⊕ arr<sub>i−1</sub>) ⊕ (arr<sub>0</sub> ⊕ arr<sub>1</sub> ⊕⋯⊕ arr<sub>i−1</sub> ⊕ arr<sub>i</sub> ⊕⋯⊕ arr<sub>j−1</sub>）

由于异或运算满足结合律和交换律，且任意数异或自身等于 00，上式可化简为:

S<sub>i</sub> ⊕ S<sub>j</sub> = (arr<sub>i</sub>  ⊕⋯⊕ arr<sub>j</sub>) 

## 代码

```java
class Solution {
    public int countTriplets(int[] arr) {
        int n = arr.length;
        int[] s = new int[n + 1];
        for (int i = 0; i < n; ++i) {
            s[i + 1] = s[i] ^ arr[i];
        }
        int ans = 0;
        for (int i = 0; i < n; ++i) {
            for (int k = i + 1; k < n; ++k) {
                if (s[i] == s[k + 1]) {
                    ans += k - i; //[i+1,k] 的范围内的任意 j 都是符合要求的，对应的三元组个数为 k-i
                }
            }
        }
        return ans;
    }
}
```



