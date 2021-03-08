---
title: 剑指 Offer 24. 反转链表
date: 2020-09-25 17:59:02
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

## 示例

> 输入: 1->2->3->4->5->NULL
> 输出: 5->4->3->2->1->NULL

<!--more-->

## 限制

0 <= 节点个数 <= 5000

## 思路

递归的两个条件：

1. 终止条件是当前节点或者下一个节点为null
2. 在函数内部，改变节点的指向，也就是 head 的下一个节点指向 head 递归函数



![](arithmetic8\5ff86a743320333d3fe335c711182de37fb0fce958a005064254b4b48b2958a9.gif)

## 代码

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        
    if (head == null || head.next == null)
        return head;
    ListNode reverse = reverseList(head.next);
    head.next.next = head;
    head.next = null;
    return reverse;

    }
}
```

