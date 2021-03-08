---
title: 剑指 Offer 05. 替换空格
date: 2020-09-23 17:19:09
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。



## 示例

> 输入：s = "We are happy."
> 输出："We%20are%20happy."

<!--more-->

## 限制

- 0 <= s 的长度 <= 10000




## 代码

```java
class Solution {
    public String replaceSpace(String s) {
        StringBuilder res = new StringBuilder();
        for(Character c : s.toCharArray())
        {
            if(c == ' ') res.append("%20");
            else res.append(c);
        }
        return res.toString();
    }
}
```

