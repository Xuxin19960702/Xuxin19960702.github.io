---
title: 第 N 位数字
date: 2021-08-16 16:25:00
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

在无限的整数序列 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ...中找到第 n 位数字。

## 示例

> 输入：11
>
> 输出：0
>
> 解释：第 11 位数字在序列 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ... 里是 0 ，它是 10 的一部分。

<!--more-->

## 限制

- n 是正数且在 32 位整数范围内（n < 2<sup>31</sup>）。

## 思路

对于第 n 位对应的数字，我们令这个数字对应的数为 target，然后分三步进行。

- 首先找到这个数字对应的数是几位数，用 digits 表示；
- 然后确定这个对应的数的数值 target；
- 最后确定返回值是 target 中的哪个数字。

## 代码

```java
class Solution {
    public int findNthDigit(int n) {
		long num=n;
		
		long size=1;
		long max=9;
		
		while(n>0){
			//判断不在当前位数内
			if(num-max*size>0){
				num=num-max*size;
				size++;
				max=max*10;
			}else{
				long count=num/size;
				long left=num%size;
				if(left==0){
					return (int) (((long)Math.pow(10, size-1)+count-1)%10);
				}else{
					return (int) (((long)Math.pow(10, size-1)+count)/((long)Math.pow(10, (size-left)))%10);
				}
			}
		}
		
		return 0;
    }
}
```



