---
title: 剑指 Offer 58 - I. 翻转单词顺序
date: 2021-07-27 23:00:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

## 示例

> 输入："the sky is blue"
>
> 输出："blue is sky the"
> 

<!--more-->

## 限制

- 无空格字符构成一个单词。
- 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
- 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。

## 思路 

 以空格为分割符完成字符串分割后，若两单词间有 x > 1 个空格，则在单词列表 strs 中，此两单词间会多出 x - 1 个 “空单词” （即 "" ）。解决方法：倒序遍历单词列表，并将单词逐个添加至 StringBuilder ，遇到空单词时跳过。

## 代码

```java
class Solution {
    public String reverseWords(String s) {
        String[] strs = s.trim().split(" "); // 删除首尾空格，分割字符串
        StringBuilder res = new StringBuilder();
        for(int i = strs.length - 1; i >= 0; i--) { // 倒序遍历单词列表
            if(strs[i].equals("")) continue; // 遇到空单词则跳过
            res.append(strs[i] + " "); // 将单词拼接至 StringBuilder
        }
        return res.toString().trim(); // 转化为字符串，删除尾部空格，并返回
    }
}
```



