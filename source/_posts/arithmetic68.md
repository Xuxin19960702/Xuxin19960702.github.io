---
title: 剑指 Offer 59 - II. 队列的最大值
date: 2021-07-30 10:42:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

请定义一个队列并实现函数 `max_value` 得到队列里的最大值，要求函数`max_value`、`push_back` 和 `pop_front` 的均摊时间复杂度都是O(1)。

若队列为空，`pop_front` 和 `max_value` 需要返回 -1

## 示例

> 输入：["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
> [[],[1],[2],[],[],[]]
>
> 输出： [null,null,null,2,1,2]

<!--more-->

## 限制

- `1 <= push_back,pop_front,max_value的总操作数 <= 10000`
- `1 <= value <= 10^5`

## 思路 

直接实现一个普通的队列，查询最大值时遍历计算。

## 代码

```java
class MaxQueue {
    int[] q = new int[20000];
    int begin = 0, end = 0;

    public MaxQueue() {

    }
    
    public int max_value() {
        int ans = -1;
        for (int i = begin; i != end; ++i) {
            ans = Math.max(ans, q[i]);
        }
        return ans;
    }
    
    public void push_back(int value) {
        q[end++] = value;
    }
    
    public int pop_front() {
        if (begin == end) {
            return -1;
        }
        return q[begin++];
    }
}
```

