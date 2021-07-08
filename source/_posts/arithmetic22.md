---
title: 剑指 Offer 31. 栈的压入、弹出序列
date: 2021-07-08 23:10:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。

## 示例

> 输入：pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
>
> 输出：true
>
> 解释：我们可以按以下顺序执行
> push(1), push(2), push(3), push(4), pop() -> 4,
> push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1

<!--more-->

## 限制

- 0 <= pushed.length == popped.length <= 1000
- 0 <= pushed[i], popped[i] < 1000
- pushed 是 popped 的排列。

## 思路 

考虑借用一个辅助栈 stack ，**模拟** 压入 / 弹出操作的排列。根据是否模拟成功，即可得到结果。

- **入栈操作：** 按照压栈序列的顺序执行。
- **出栈操作：** 每次入栈后，循环判断 “栈顶元素 == 弹出序列的当前元素” 是否成立，将符合弹出序列顺序的栈顶元素全部弹出。

> 由于题目规定 栈的所有数字均不相等 ，因此在循环入栈中，每个元素出栈的位置的可能性是唯一的（若有重复数字，则具有多个可出栈的位置）。因而，在遇到 “栈顶元素 == 弹出序列的当前元素” 就应立即执行出栈。

**算法流程：**

1. **初始化：** 辅助栈 *stack* ，弹出序列的索引 i ；
2. **遍历压栈序列：** 各元素记为 *num* ；
   1. 元素 *num* 入栈；
   2. 循环出栈：若 *stack* 的栈顶元素 == 弹出序列元素 *popped*[i] ，则执行出栈与 i++ ；
3. **返回值：** 若 *stack* 为空，则此弹出序列合法。

## 代码

```java
class Solution {
    public boolean validateStackSequences(int[] pushed, int[] popped) {
        Stack<Integer> stack = new Stack<>();
        int i = 0;
        for(int num : pushed) {
            stack.push(num); // num 入栈
            while(!stack.isEmpty() && stack.peek() == popped[i]) { // 循环判断与出栈
                stack.pop();
                i++;
            }
        }
        return stack.isEmpty(); // 如果为空返回true，反之false
    }
}
```



