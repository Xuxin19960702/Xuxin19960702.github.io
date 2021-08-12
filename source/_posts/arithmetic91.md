---
title: 反转字符串中的单词 III
date: 2021-08-12 18:32:00
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

给定一个字符串，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

## 示例

> 输入："Let's take LeetCode contest"
>
> 输出："s'teL ekat edoCteeL tsetnoc"
>

<!--more-->

## 限制

- 在字符串中，每个单词由单个空格分隔，并且字符串中不会有任何额外的空格。

## 思路

把字符串转成字符数组，遍历字符数组；
我们只关心空格字符和最后一个字符，于是，遇到正常的字母字符一概不管；
当遇到空格字符，就需要对刚刚遍历过的单词进行反转操作，此单词的右索引是 i - 1，如何获取左索引？定义一个int变量start，用来记录单词的左索引；
利用字符数组前后交换字符位置的方法进行反转操作；反转结束后，把start索引置为 i + 1，指向下一个单词的开头；
遍历继续，直到遇到下一个空格字符或结尾；
到了字符数组结尾，那么最后一个单词的开头和结束索引分别是 start 和 n - 1，利用这两个索引进行单词翻转；
最后用String的构造方法，将char数组转成答案返回。

## 代码

```java
class Solution {
    public String reverseWords(String s) {
        char[] array = s.toCharArray();
        int start = 0;
        for (int i = 0; i < array.length; i++) {
            if (array[i] == ' ') {
                reverse(array, start, i - 1);
                start = i + 1; // 更新start为下一个单词的左索引
                continue;
            }
            if (i == array.length - 1) {
                reverse(array, start, i);
            }
        }
        return new String(array);
    }

    private void reverse(char[] array, int l, int r) {
        while (l < r) {
            char temp = array[l];
            array[l] = array[r];
            array[r] = temp;
            l += 1;
            r -= 1;
        }
    }
}
```



