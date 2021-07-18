---
title: 剑指 Offer 35. 复杂链表的复制
date: 2021-07-17 23:35:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。

## 示例

> 输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
>
> 输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]

<!--more-->

## 限制

- `-10000 <= Node.val <= 10000`
- `Node.random` 为空（null）或指向链表中的节点。
- 节点数目不超过 1000 。

## 思路 

**方法一（哈希表）：**

1. 若头节点 head 为空节点，直接返回 nullnull ；
2. **初始化：** 哈希表 dic ， 节点 cur 指向头节点；
3. **复制链表：**
   - 建立新节点，并向 dic 添加键值对 (原 cur 节点, 新 cur 节点） ；
   - cur 遍历至原链表下一节点；
4. **构建新链表的引用指向：**
   - 构建新节点的 next 和 random 引用指向；
   - cur 遍历至原链表下一节点；
5. **返回值：** 新链表的头节点 dic[cur] ；



**方法二（拼接+拆分）**

1. **复制各节点，构建拼接链表:**
   - 设原链表为 node1→node2→⋯ ，构建的拼接链表如下所示：

​                           node1→node1 new→node2→node2 new→⋯

2. **构建新链表各节点的 random 指向：**
   - 当访问原节点 cur 的随机指向节点 cur.random 时，对应新节点 cur.next 的随机指向节点为 cur.random.next 。

3. **拆分原 / 新链表：**
   - 设置 pre / cur 分别指向原 / 新链表头节点，遍历执行 pre.next = pre.next.next 和 cur.next = cur.next.next 将两链表拆分开。

4. 返回新链表的头节点 res 即可。

## 代码

```java
// 方法一（哈希表）
class Solution {
    public Node copyRandomList(Node head) {
        if(head == null) return null;
        Node cur = head;
        Map<Node, Node> map = new HashMap<>();
        // 3. 复制各节点，并建立 “原节点 -> 新节点” 的 Map 映射
        while(cur != null) {
            map.put(cur, new Node(cur.val));
            cur = cur.next;
        }
        cur = head;
        // 4. 构建新链表的 next 和 random 指向
        while(cur != null) {
            map.get(cur).next = map.get(cur.next);
            map.get(cur).random = map.get(cur.random);
            cur = cur.next;
        }
        // 5. 返回新链表的头节点
        return map.get(head);
    }
}
```

```java
// 方法二（拼接+拆分）
class Solution {
    public Node copyRandomList(Node head) {
        if(head == null) return null;
        Node cur = head;
        // 1. 复制各节点，并构建拼接链表
        while(cur != null) {
            Node tmp = new Node(cur.val);
            tmp.next = cur.next;
            cur.next = tmp;
            cur = tmp.next;
        }
        // 2. 构建各新节点的 random 指向
        cur = head;
        while(cur != null) {
            if(cur.random != null)
                cur.next.random = cur.random.next;
            cur = cur.next.next;
        }
        // 3. 拆分两链表
        cur = head.next;
        Node pre = head, res = head.next;
        while(cur.next != null) {
            pre.next = pre.next.next;
            cur.next = cur.next.next;
            pre = pre.next;
            cur = cur.next;
        }
        pre.next = null; // 单独处理原链表尾节点
        return res;      // 返回新链表头节点
    }
}
```

