---
title: 剑指 Offer 50. 第一个只出现一次的字符
date: 2021-07-21 22:08:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

## 示例

> 输入："abaccdeff"
>
> 输出："b"

<!--more-->

## 限制

- 0 <= s 的长度 <= 50000

## 思路 

1. **初始化：** HashMap，记为 dic ；
2. **字符统计：** 遍历字符串 s 中的每个字符 c ；
   - 若 dic 中 **不包含** 键(key) c ：则向 dic 中添加键值对 (c, True) ，代表字符 c 的数量为 1 ；
   - 若 dic 中 **包含** 键(key) c ：则修改键 c 的键值对为 (c, False) ，代表字符 c 的数量 > 1。
3. **查找数量为 1 的字符：** 遍历字符串 s 中的每个字符 c ；
   - 若 dic中键 c 对应的值为 True ：，则返回 c 。
4. 返回 ' ' ，代表字符串无数量为 1 的字符。

## 代码

```java
class Solution {
    public char firstUniqChar(String s) {
        HashMap<Character, Boolean> dic = new HashMap<>();
        char[] sc = s.toCharArray();
        for(char c : sc)
            dic.put(c, !dic.containsKey(c));
        for(char c : sc)
            if(dic.get(c)) return c;
        return ' ';
    }
}
```

