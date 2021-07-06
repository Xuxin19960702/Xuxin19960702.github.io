---
title: 删除链表的倒数第 N 个结点
date: 2021-07-05 17:30:02
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

## 示例

> 输入: head = [1,2,3,4,5], n = 2
>
> 输出: [1,2,3,5]

<!--more-->

## 限制

- 链表中结点的数目为 `sz`
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`

## 思路

递归，反求后第几位

## 代码

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 * 方法一：先遍历一遍得到链表长度
 * 方法二：用栈弹出
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        int traverse = traverse(head, n);
    	if(traverse == n)
    	    return head.next;
    	return head;
    }
    
    private int traverse(ListNode node, int n) {
        if(node == null)
            return 0;
        int num = traverse(node.next, n);
        if(num == n)
            node.next = node.next.next;
        return num + 1;
    }
}
```

