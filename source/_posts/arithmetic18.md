---
title: 剑指 Offer 05. 替换空格
date: 2021-07-07 22:38:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

## 示例

> 输入：s = "We are happy."
>
> 输出："We%20are%20happy."

<!--more-->

## 限制

- 0 <= s 的长度 <= 10000

## 思路 

我们可以通过循环判断字符串的字符是否为空格，是的话就利用append()方法添加追加“%20”，否则还是追加原字符

或者最简单的方法就是利用：replaceAll(String regex, String replacement)方法了

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

```java
import java.util.Scanner;
/**
 * 一行代码解决
 * \ 转义字符。如果你要使用 "\" 本身，则应该使用 "\\"。String类型中的空格用"\s"表示，所以这里"\\s"就是代表空格的意思
 */
public class replaceSpace {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String s = scanner.nextLine();
        System.out.println(replaceSpace(s));
    }

    public static String replaceSpace(String s) {
        StringBuilder res = new StringBuilder(s);
        return res.toString().replaceAll("\\s","%20");
    }
}

```

