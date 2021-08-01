---
title: 剑指 Offer 59 - I. 滑动窗口的最大值
date: 2021-08-01 23:55:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

给定一个数组 `nums` 和滑动窗口的大小 `k`，请找出所有滑动窗口里的最大值。

## 示例

> 输入：nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
> 
>输出： [3,3,5,5,6,7] 

<!--more-->

## 限制

- 你可以假设 *k* 总是有效的，在输入数组不为空的情况下，1 ≤ k ≤ 输入数组的大小。

## 思路

1. **初始化：** 双端队列 deque ，结果列表 res ，数组长度 n ；
2. **滑动窗口：** 左边界范围 i∈[1−k,n−k] ，右边界范围 j∈[0,n−1] ；
   1. 若 i > 0 且 队首元素 deque[0] = 被删除元素 nums[i - 1]nums[i−1] ：则队首元素出队；
   2. 删除 deque 内所有 <nums[j] 的元素，以保持 deque 递减；
   3. 将 nums[j] 添加至 deque 尾部；
   4. 若已形成窗口（即 i≥0 ）：将窗口最大值（即队首元素 deque[0]）添加至列表 res ；
3. **返回值：** 返回结果列表 res ；

## 代码

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(nums.length == 0 || k == 0) return new int[0];
        Deque<Integer> deque = new LinkedList<>();
        int[] res = new int[nums.length - k + 1];
        for(int j = 0, i = 1 - k; j < nums.length; i++, j++) {
            // 删除 deque 中对应的 nums[i-1]
            if(i > 0 && deque.peekFirst() == nums[i - 1])
                deque.removeFirst();
            // 保持 deque 递减
            while(!deque.isEmpty() && deque.peekLast() < nums[j])
                deque.removeLast();
            deque.addLast(nums[j]);
            // 记录窗口最大值
            if(i >= 0)
                res[i] = deque.peekFirst();
        }
        return res;
    }
}
```

