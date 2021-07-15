---
title: 剑指 Offer 15. 二进制中1的个数
date: 2021-07-15 23:37:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

编写一个函数，输入是一个无符号整数（以二进制串的形式），返回其二进制表达式中数字位数为 '1' 的个数（也被称为 [汉明重量](http://en.wikipedia.org/wiki/Hamming_weight)).）。

## 示例

> 输入：n = 11 (控制台输入 00000000000000000000000000001011)
>
> 输出：3
>
> 解释：输入的二进制串 00000000000000000000000000001011 中，共有三位为 '1'。

<!--more-->

## 限制

- 输入必须是长度为 `32` 的 **二进制串** 。

## 思路 

方法一：

1. 初始化数量统计变量 res = 0 。
2. 循环逐位判断： 当 n = 0 时跳出。
   - res += n & 1 ： 若 n \& 1 = 1，则统计数 res 加一。
   - n >>= 1 ： 将二进制数字 n 无符号右移一位（ Java 中无符号右移为 ">>>" ） 。
3. 返回统计数量res

方法二：

1. 初始化数量统计变量 res 。
2. 循环消去最右边的 1 ：当 n = 0 时跳出。
   - res += 1 ： 统计变量加 1 ；
   - n &= n - 1 ： 消去数字 n 最右边的 1 。

3. 返回统计数量 res 。

## 代码

```java
//方法一
public class Solution {
    public int hammingWeight(int n) {
        int res = 0;
        while(n != 0) {
            res += n & 1;
            n >>>= 1;
        }
        return res;
    }
}
```

```java
//方法二
public class Solution {
    public int hammingWeight(int n) {
        int res = 0;
        while(n != 0) {
            res++;
            n &= n - 1;
        }
        return res;
    }
}
```

