---
title: 剑指 Offer 48. 最长不含重复字符的子字符串
date: 2021-07-28 11:07:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

## 示例

> 输入："abcabcbb"
>
> 输出：3
>
> 解释：因为无重复字符的最长子串是 "abc"，所以其长度为 3。

<!--more-->

## 限制

- `s.length <= 40000`

## 思路 

![](arithmetic62/Picture1.png)

## 代码

```java
// 双指针 + 哈希表
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> dic = new HashMap<>();
        int i = -1, res = 0;
        for(int j = 0; j < s.length(); j++) {
            if(dic.containsKey(s.charAt(j)))
                i = Math.max(i, dic.get(s.charAt(j))); // 更新左指针 i
            dic.put(s.charAt(j), j); // 哈希表记录
            res = Math.max(res, j - i); // 更新结果
        }
        return res;
    }
}
```

```java
// 动态规划 + 哈希表
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> dic = new HashMap<>();
        int res = 0, tmp = 0;
        for(int j = 0; j < s.length(); j++) {
            int i = dic.getOrDefault(s.charAt(j), -1); // 获取索引 i
            dic.put(s.charAt(j), j); // 更新哈希表
            tmp = tmp < j - i ? tmp + 1 : j - i; // dp[j - 1] -> dp[j]
            res = Math.max(res, tmp); // max(dp[j - 1], dp[j])
        }
        return res;
    }
}
```

