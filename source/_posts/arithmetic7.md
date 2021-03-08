---
title: 剑指 Offer 06. 从尾到头打印链表
date: 2020-09-23 17:48:32
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。



## 示例

> 输入：head = [1,3,2]
> 输出：[2,3,1]

<!--more-->

## 限制

- 0 <= 链表长度 <= 10000



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
   ArrayList<Integer> tmp = new ArrayList<Integer>();

    public int[] reversePrint(ListNode head) {
        recur(head);
        int[] res = new int[tmp.size()];
        for(int i = 0; i < res.length; i++)
            res[i] = tmp.get(i);
        return res;
    }

    void recur(ListNode head) {
        if(head == null) return;
        recur(head.next);
        tmp.add(head.val);
    }
}
```

