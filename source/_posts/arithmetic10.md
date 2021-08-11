---
title: 最长回文子序列
date: 2021-06-29 17:59:02
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

给定一个字符串 `s` ，找到其中最长的回文子序列，并返回该序列的长度。可以假设 `s` 的最大长度为 `1000` 。

## 示例

> 输入: "bbbab"
> 输出: 4

一个可能的最长回文子序列为 "bbbb"。

<!--more-->

## 限制

1 <= s.length <= 1000

s 只包含小写英文字母

## 思路

动态规划，如下代码注释。

[LeetCode题解](https://leetcode-cn.com/problems/longest-palindromic-subsequence/solution/zi-xu-lie-wen-ti-tong-yong-si-lu-zui-chang-hui-wen/)

## 代码

```java
class Solution {
    public int longestPalindromeSubseq(String s) {
        /*
            bb aa bb
            bb a  bb
            dp[i][j] 表示 第 i 个字符到 第 j 个字符之间最长的回文子序列长度
            1、当 s[i] == s[j] 时，考虑 i 和 j 中间序列的奇偶个数， dp[i][j] = dp[i+1][j-1] + 2
            对上述 dp[i][j] =  dp[i+1][j-1] + 2 的解释：
            当序列为 b aa b 时， i = 0, j = 3，则 dp[0][3] = dp[1][2] + 2 = 4
            当序列为 b a b 时，i = 0, j = 2，则 dp[0][2] = dp[1][1] + 2 = 3 
            当序列为 b b 时， i = 0, j = 1，则 dp[0][1] = dp[1][0] = 0 + 2 = 2 (dp[1][0] 默认值为 0)
            该式子同时考虑到了奇偶
            2、当 s[i] != s[j] ，那么 dp[i][j] = Math.max(dp[i+1][j],dp[i][j-1])
            对上述 dp[i][j] 式子的解释：
            假如序列为 d c b c c（index：0-4），s[0] != s[4] ，则 dp[0][4] = Math.max(dp[0][3],dp[1,4]) = Math.max(2,3) = 3
        */

        nt n = s.length();
        int[][] f = new int[n][n];
        for (int i = n - 1; i >= 0; i--) {
            f[i][i] = 1;
            for (int j = i + 1; j < n; j++) {
                if (s.charAt(i) == s.charAt(j)) {
                    f[i][j] = f[i + 1][j - 1] + 2;
                } else {
                    f[i][j] = Math.max(f[i + 1][j], f[i][j - 1]);
                }
            }
        }
        return f[0][n - 1];
    }
}
```

