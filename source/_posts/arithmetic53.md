---
title: 剑指 Offer 45. 把数组排成最小的数
date: 2021-07-24 23:36:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

## 示例

> 输入： [3,30,34,5,9]
>
>    输出："3033459"

<!--more-->

## 限制

- `0 < nums.length <= 100`

## 思路 

此题求拼接起来的最小数字，本质上是一个排序问题。设数组 nums 中任意两数字的字符串为 x 和 y ，则规定 排序判断规则 为：

- 若拼接字符串 x + y > y + x，则 x “大于” y ；
- 反之，若 x + y < y + x，则 x “小于” y ； 

1. **初始化：** 字符串列表 strs ，保存各数字的字符串格式；
2. **列表排序：** 应用以上 “排序判断规则” ，对 strs 执行排序；
3. **返回值：** 拼接 strs 中的所有字符串，并返回。



## 代码

```java
class Solution {
    public String minNumber(int[] nums) {
        String[] strs = new String[nums.length];
        for(int i = 0; i < nums.length; i++)
            strs[i] = String.valueOf(nums[i]);
        Arrays.sort(strs, (x, y) -> (x + y).compareTo(y + x));
        StringBuilder res = new StringBuilder();
        for(String s : strs)
            res.append(s);
        return res.toString();
    }
}
```



