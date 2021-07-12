---
title: 剑指 Offer 10- II. 变态青蛙跳台阶问题
date: 2021-07-06 23:20:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶 …… 它也可以跳上n级。求该青蛙跳上一个 `n` 级的台阶总共有多少种跳法。

## 示例

> 输入: n = 2
>
> 输出: 2

<!--more-->

## 限制

- 0 <= n <= 100

## 思路

假设 n ≧ 2，第一步有n种跳法：跳1级、跳2级、到跳n级。跳1级，剩下n-1级，则剩下跳法是 f(n-1) ；跳2级，剩下跳法是 f(n-2)……跳n-1级，剩下1级，则剩下跳法是 f(1) ；跳n级，剩下0级，则剩下跳法是 f(0) 。所以在 n ≧ 2 的情况下：f(n) = f(n-1) + f(n-2) + …… + f(1) ， 因为 f(n-1) = f(n-2) + f(n-3) + …… + f(1) ，所以 f(n) = 2 * f(n-1)。又f(1)  = 1, 所以可得 f(n) = 2<sup>n-1</sup>。

## 代码

```java
public class JumpFloorII {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        System.out.println(JumpFloorII(n));
    }

    static int JumpFloorII(int number){
        return 1 << --number; //2^(number-1)用位移操作进行，更快
    }
}
```

### 补充

Java 中有三种位移运算符：

1. “<<”：左位移运算符，等同于乘2的n次方
2. “>>”：右位移运算符，等同于除2的n次方
3. “>>>”：无符号右移运算符，不管移动前最高位是0还是1，右移后左侧产生的空位部分都以0来填充。与>>类似。例：int a = 16; int b = a << 2；//左移2，等同于16 * 2 的2次方，也就是16 * 4。int c= a >> 2;//右移2，等同于16 / 2 的2次方，也就是16 / 4。

