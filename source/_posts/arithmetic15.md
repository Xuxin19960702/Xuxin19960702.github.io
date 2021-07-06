---
title: 剑指 Offer 10- II. 青蛙跳台阶问题
date: 2021-07-06 22:54:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 `n` 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

## 示例

> 输入: n = 2
>
> 输出: 2

<!--more-->

## 限制

- 0 <= n <= 100

## 思路

> 此类求 *多少种可能性* 的题目一般都有 **递推性质** ，即 f(n)*f*(*n*) 和 f(n-1)*f*(*n*−1)…f(1)*f*(1) 之间是有联系的。

- 设跳上 n 级台阶有 f(n) 种跳法。在所有跳法中，青蛙的最后一步只有两种情况： 跳上 1 级或 2 级台阶。
  1. 当为 1 级台阶： 剩 n-1 个台阶，此情况共有 f(n-1) 种跳法；
  2. 当为 2 级台阶： 剩 n-2 个台阶，此情况共有 f(n-2) 种跳法。
- f(n) 为以上两种情况之和，即 f(n)=f(n-1)+f(n-2) ，以上递推性质为斐波那契数列。本题可转化为 求斐波那契数列第 n 项的值 ，与 剑指 Offer 10- I. 斐波那契数列 等价，唯一的不同在于起始数字不同。
  青蛙跳台阶问题： f(0)=1 , f(1)=1 , f(2)=2 ；
  斐波那契数列问题： f(0)=0 , f(1)=1 , f(2)=1 。

## 代码

```java
/**
 * 动态规划方法
 */
class Solution {
    public int fib(int n) {
        int a = 1, b = 1, sum;
        for(int i = 0; i < n; i++){
            sum = (a + b) % 1000000007;
            a = b;
            b = sum;
        }
        return a;
    }
}
```

```java
/**
 * 递归方法 这个方法取模有问题
 */
public class Fibonacci {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        System.out.println(Fibonacci(n));
    }

    public static int Fibonacci(int n) {
        if (n == 0 || n == 1) {
            return 1;
        }
        if (n == 2) {
            return 2;
        }
        return Fibonacci(n - 1) + Fibonacci(n - 2);
    }
}
```

