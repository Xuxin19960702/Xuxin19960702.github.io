---
title: 最长回文子串
date: 2021-06-28 17:59:02
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

给你一个字符串 `s`，找到 `s` 中最长的回文子串。

## 示例

> 输入: s = "babad"
> 输出: "bab"

<!--more-->

## 限制

1 <= s.length <= 1000

s` 仅由数字和英文字母（大写和/或小写）组成

## 思路

我们仔细观察一下方法一中的状态转移方程：

$$
\begin{cases}
P(i,i) & = & true \\
P(i,i+1) & = & (S_i == S_{i+1}) \\
P(i,j) & = & P(i+1,j-1) \bigwedge (S_i == S_j)
\end{cases}
$$
找出其中的状态转移链：
P(i,j) ← P(i+1,j−1) ← P(i+2,j−2) ← ⋯ ← 某一边界情况

可以发现，所有的状态在转移的时候的可能性都是唯一的。也就是说，我们可以从每一种边界情况开始「扩展」，也可以得出所有的状态对应的答案。

边界情况即为子串长度为 11 或 22 的情况。我们枚举每一种边界情况，并从对应的子串开始不断地向两边扩展。如果两边的字母相同，我们就可以继续扩展，例如从 P(i+1,j-1)P(i+1,j−1) 扩展到 P(i,j)P(i,j)；如果两边的字母不同，我们就可以停止扩展，因为在这之后的子串都不能是回文串了。

聪明的读者此时应该可以发现，「边界情况」对应的子串实际上就是我们「扩展」出的回文串的「回文中心」。方法二的本质即为：我们枚举所有的「回文中心」并尝试「扩展」，直到无法扩展为止，此时的回文串长度即为此「回文中心」下的最长回文串长度。我们对所有的长度求出最大值，即可得到最终的答案。



## 代码

```java
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() < 1) {
            return "";
        }
        int start = 0, end = 0;
        for (int i = 0; i < s.length(); i++) {
            int len1 = expandAroundCenter(s, i, i);
            int len2 = expandAroundCenter(s, i, i + 1);
            int len = Math.max(len1, len2);
            if (len > end - start) {
                start = i - (len - 1) / 2;
                end = i + len / 2;
            }
        }
        return s.substring(start, end + 1);
    }

    public int expandAroundCenter(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            --left;
            ++right;
        }
        return right - left - 1;
    }
}
```

