---
title: 剑指offer 58 - II.左旋转字符串  
subtitle: 一天一题
date: 2020-07-27 22:32:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---
## 题目

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。




## 示例1
> 输入：s = "abcdef", k = 2
> 输出："cdefgab"

## 示例2
> 输入：s = "lrloseumgh", k = 6
> 输出："umghlrlose"

<!--more-->

## 限制
 - 1 <= k < s.length <= 10000



## 解法
```java
	class Solution {
	    public String reverseLeftWords(String s, int n) {
	        return s.substring(n) + s.substring(0,n);
	    }
	}
```