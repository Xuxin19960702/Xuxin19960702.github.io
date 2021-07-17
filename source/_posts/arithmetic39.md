---
title: 剑指 Offer 18. 删除链表的节点
date: 2021-07-17 23:26:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。

## 示例

> 输入：head = [4,5,1,9], val = 5
>
> 输出：[4,1,9]
>
> 解释：给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.

<!--more-->

## 限制

- 题目保证链表中节点的值互不相同

## 思路 

1. 特例处理： 当应删除头节点 head 时，直接返回 head.next 即可。
2. 初始化： pre = head , cur = head.next 。
3. 定位节点： 当 cur 为空 或 cur 节点值等于 val 时跳出。
   - 保存当前节点索引，即 pre = cur 。
   - 遍历下一节点，即 cur = cur.next 。
4. 删除节点： 若 cur 指向某节点，则执行 pre.next = cur.next ；若 cur 指向 null ，代表链表中不包含值为 val 的节点。
5. 返回值： 返回链表头部节点 head 即可。

## 代码

```java
class Solution {
    public ListNode deleteNode(ListNode head, int val) {
        if(head.val == val) return head.next;
        ListNode pre = head, cur = head.next;
        while(cur != null) {
            if(cur.val == val) break;
            pre = cur;
            cur = cur.next;
        }
        if(cur != null) pre.next = cur.next;
        return head;
    }
}
```



