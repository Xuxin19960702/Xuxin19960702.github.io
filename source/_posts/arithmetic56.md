---
title: 剑指 Offer 52. 两个链表的第一个公共节点
date: 2021-07-26 23:33:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

输入两个链表，找出它们的第一个公共节点。

## 示例

> 输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
>
> 输出：Reference of the node with value = 8
>
> 解释：相交节点的值为 8 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
>

<!--more-->

## 限制

- 如果两个链表没有交点，返回 null.
- 在返回结果后，两个链表仍须保持原有的结构。
- 可假定整个链表结构中没有循环。
- 程序尽量满足 O(n) 时间复杂度，且仅用 O(1) 内存。

## 思路 

情况一：两个链表相交

链表 headA 和 headB 的长度分别是 m 和 n。假设链表headA 的不相交部分有 a 个节点，链表 headB 的不相交部分有 b 个节点，两个链表相交的部分有 c 个节点，则有 a+c=m，b+c=n。

- 如果 a=b，则两个指针会同时到达两个链表的第一个公共节点，此时返回两个链表的第一个公共节点；
- 如果 a/b，则指针 pA 会遍历完链表 headA，指针 pB 会遍历完链表 headB，两个指针不会同时到达链表的尾节点，然后指针 pA 移到链表 headB 的头节点，指针 pB 移到链表 headA 的头节点，然后两个指针继续移动，在指针 pA 移动了 a+c+b 次、指针 pB 移动了 b+c+a 次之后，两个指针会同时到达两个链表的第一个公共节点，该节点也是两个指针第一次同时指向的节点，此时返回两个链表的第一个公共节点。

情况二：两个链表不相交

链表 headA 和 headB 的长度分别是 m 和 n。考虑当 m = n 和 m / n 时，两个指针分别会如何移动：

- 如果 m = n，则两个指针会同时到达两个链表的尾节点，然后同时变成空值 null，此时返回 null；
- 如果 m / n，则由于两个链表没有公共节点，两个指针也不会同时到达两个链表的尾节点，因此两个指针都会遍历完两个链表，在指针 pA 移动了 m+n 次、指针 pB 移动了 n+m 次之后，两个指针会同时变成空值 null，此时返回 null。

## 代码

```java
// 方法一 使用哈希集合存储链表节点
// 时间复杂度：O(m+n)
// 空间复杂度：O(m)
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        Set<ListNode> visited = new HashSet<ListNode>();
        ListNode temp = headA;
        while (temp != null) {
            visited.add(temp);
            temp = temp.next;
        }
        temp = headB;
        while (temp != null) {
            if (visited.contains(temp)) {
                return temp;
            }
            temp = temp.next;
        }
        return null;
    }
}
```

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) {
            return null;
        }
        ListNode pA = headA, pB = headB;
        while (pA != pB) {
            pA = pA == null ? headB : pA.next;
            pB = pB == null ? headA : pB.next;
        }
        return pA;
    }
}
```

