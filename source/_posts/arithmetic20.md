---
title: 剑指 Offer 21. 调整数组顺序使奇数位于偶数前面
date: 2021-07-08 20:09:00
categories: 算法题
archives:
tags: [Java,算法,剑指offer]
---

## 题目

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。

## 示例

> 输入：nums = [1,2,3,4]
>
> 输出：[1,3,2,4]
>
> 注：[3,1,2,4] 也是正确的答案之一。

<!--more-->

## 限制

- 0 <= nums.length <= 50000
- 1 <= nums[i] <= 10000

## 思路 

思路一：`头尾双指针`

- left指向数组头，right指向数组尾
- left右移直到指向了偶数
- right左移直到指向了奇数
- 如果left此时已经大于right，break结束循环
- 交换left和right所指数字
- 继续以上步骤，直到left > right



思路二：`快慢指针`

- slow和fast都从数组的头部开始遍历
- fast正常一步一步右移
- 如果fast遇到了奇数，和slow位置的数字互换，slow++，fast++
- 如果fast没有遇到奇数，继续右移，fast++
- fast遍历到末尾时结束遍历

## 代码

```java
// 思路一
class Solution {
    public int[] exchange(int[] nums) {
        int left = 0, right = nums.length - 1;
        while(left <= right){
            while(left <= right && nums[left] % 2 == 1)
                left++;
            while(left <= right && nums[right] % 2 == 0)
                right--;
            if(left > right)
                break;
            int tmp = nums[left];
            nums[left] = nums[right];
            nums[right] = tmp;
        }
        return nums;
    }
}
```



```java
// 思路二
class Solution {
    public int[] exchange(int[] nums) {
        int slow = 0, fast = 0;
        while(fast < nums.length){
            if(nums[fast] % 2 == 1){
                int tmp = nums[slow];
                nums[slow] = nums[fast];
                nums[fast] = tmp;
                slow++;
            }
            fast++;
        }
        return nums;
    }
}
```

