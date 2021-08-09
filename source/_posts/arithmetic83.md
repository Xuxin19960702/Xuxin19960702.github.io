---
title: 确定两个字符串是否接近
date: 2021-08-08 19:46:00
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

如果可以使用以下操作从一个字符串得到另一个字符串，则认为两个字符串 接近 ：

- 操作 1：交换任意两个 现有 字符。

  - 例如，abcde -> aecdb

- 操作 2：将一个 现有 字符的每次出现转换为另一个 现有 字符，并对另一个字符执行相同的操作。

  - 例如，aacabb -> bbcbaa（所有 a 转化为 b ，而所有的 b 转换为 a ）

  你可以根据需要对任意一个字符串多次使用这两种操作。

给你两个字符串，word1 和 word2 。如果 word1 和 word2 接近 ，就返回 true ；否则，返回 false 。

## 示例

> 输入：word1 = "cabbba", word2 = "abbccc"
>
> 输出：true
>
> 解释：3 次操作从 word1 获得 word2 。
> 执行操作 1："cabbba" -> "caabbb"
> 执行操作 2："caabbb" -> "baaccc"
> 执行操作 2："baaccc" -> "abbccc"

<!--more-->

## 限制

- `1 <= word1.length, word2.length <= 105`
- `word1` 和 `word2` 仅包含小写英文字母

## 思路

把题目要求翻译成人话就是，
如果两个字符串：

- 包含的字符种类完全一样；
- 把各个字符的重复次数放在一个数组里，数组在排序后完全一样；

那么这两个字符串接近。

所以：

- 如果两个字符串长度不一样，那么直接返回false；
- 遍历两个字符串，用两个长度 26 的数组存放次数；
- 同时遍历这两个数组，如果在某下标 i 处出现一个是 0 一个不是 0（即异或结果是 1）的情况，那么直接返回false；
- 排序后如果数组不相同，也返回false；
- 否则返回true。

## 代码

```java
class Solution {
    public boolean closeStrings(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        if(m!=n) return false;
        
        int[] l1 = new int[26];
        int[] l2 = new int[26];

        for(int i = 0; i < m; ++i){
            ++l1[word1.charAt(i) - 'a'];
            ++l2[word2.charAt(i) - 'a'];
        }
        for(int i = 0; i < 26; ++i){
            if((l1[i] == 0) ^ (l2[i] == 0))
                return false; 
        }

        Arrays.sort(l1);
        Arrays.sort(l2);
        for(int i = 0; i < 26; ++i){
            if(l1[i] != l2[i]) return false;
        }
        return true;
    }
}
```



