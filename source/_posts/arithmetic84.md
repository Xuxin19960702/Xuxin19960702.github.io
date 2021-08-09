---
title: 长按键入
date: 2021-08-09 15:14:00
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

你的朋友正在使用键盘输入他的名字 name。偶尔，在键入字符 c 时，按键可能会被长按，而字符可能被输入 1 次或多次。

你将会检查键盘输入的字符 typed。如果它对应的可能是你的朋友的名字（其中一些字符可能被长按），那么就返回 True。

## 示例

> 输入：name = "alex", typed = "aaleex"
>
> 输出：true
>
> 解释：'alex' 中的 'a' 和 'e' 被长按。

<!--more-->

## 限制

- `name.length <= 1000`
- `typed.length <= 1000`
- `name` 和 `typed` 的字符都是小写字母。

## 思路

![](arithmetic84/1.gif)

## 代码

```java
class Solution {
    public boolean isLongPressedName(String name, String typed) {
        int i = 0, j = 0;
        while (j < typed.length()) {
            if (i < name.length() && name.charAt(i) == typed.charAt(j)) {
                i++;
                j++;
            } else if (j > 0 && typed.charAt(j) == typed.charAt(j - 1)) {
                j++;
            } else {
                return false;
            }
        }
        return i == name.length();
    }
}
```



