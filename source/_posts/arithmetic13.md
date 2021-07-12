---
title: 剑指 Offer 25. 合并两个排序的链表
date: 2021-07-05 17:45:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

## 示例

> 输入: 1 → 2 → 4, 1 → 3 → 4
>
> 输出: 1 → 1 → 2 → 3 → 4 → 4

<!--more-->

## 限制

- 0 <= 链表长度 <= 1000

## 思路

1. **初始化：** 伪头节点 *dum* ，节点 *cur* 指向 *dum*。
2. **循环合并：** 当 l<sub>1</sub> 或 l<sub>2</sub> 为空时跳出；
   1. 当 l<sub>1</sub>.val < l<sub>2</sub>.val 时：*cur* 的后继节点指定为 l<sub>1</sub>，并 l<sub>1</sub> 向前走一步；
   2. 当 l<sub>1</sub>.val ≧ l<sub>2</sub>.val 时：*cur* 的后继节点指定为 l<sub>2</sub>，并 l<sub>2</sub> 向前走一步；
   3. 节点 *cur* 向前走一步， 即 *cur* = *cur.next*。
3. **合并剩余尾部：** 跳出时有两种情况，即  l<sub>1</sub>  为空 **或**  l<sub>2</sub>  为空。
   1. 若 l<sub>1</sub>  ≠ null：将 l<sub>1</sub> 添加至节点 *cur* 之后；
   2. 否则：将 l<sub>2</sub> 添加至节点 *cur* 之后。

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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dum = new ListNode(0), cur = dum;
        while(l1 != null && l2 != null) {
            if(l1.val < l2.val) {
                cur.next = l1;
                l1 = l1.next;
            }
            else {
                cur.next = l2;
                l2 = l2.next;
            }
            cur = cur.next;
        }
        cur.next = l1 != null ? l1 : l2;
        return dum.next;
    }
}
```

