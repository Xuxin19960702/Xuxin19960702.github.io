---
title: 剑指 Offer 46. 把数字翻译成字符串
date: 2021-07-25 23:33:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

## 示例

> 输入：12258
>
> 输出：5
>
> 解释：12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"

<!--more-->

## 限制

- `0 <= num < 231`

## 思路 

动态规划：*f*(*i*)=*f*(*i*−1)+*f*(*i*−2)

## 代码

```java
class Solution {
    public int translateNum(int num) {
        char[] ch = String.valueOf(num).toCharArray();
        int len = ch.length;
        int[] dp = new int[len + 1];
        dp[0] = 1;
        dp[1] = 1;
        for(int i = 2; i <= len; i++){
            int n = (ch[i - 2] - '0') * 10 + (ch[i - 1] - '0');
            if(n >= 10 && n <= 25){
                dp[i] = dp[i - 1] + dp[i - 2];
            }else{
                dp[i] = dp[i - 1];
            }
        }
        return dp[len];
    }
}
```



