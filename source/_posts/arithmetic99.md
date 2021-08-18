---
title: 无重复字符的最长子串
date: 2021-08-18 17:20:00
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度。

## 示例

> 输入：s = "abcabcbb"
>    
>输出：3
> 
>解释：因为无重复字符的最长子串是 "abc"，所以其长度为 3。
> 

<!--more-->

## 限制

- `0 <= s.length <= 5 * 104`
- `s` 由英文字母、数字、符号和空格组成

## 思路

暴力解法时间复杂度较高，会达到 O(n<sup>2</sup>)，故而采取滑动窗口的方法降低时间复杂度
定义一个 map 数据结构存储 (k, v)，其中 key 值为字符，value 值为字符位置 +1，加 1 表示从字符位置后一个才开始不重复
我们定义不重复子串的开始位置为 start，结束位置为 end
随着 end 不断遍历向后，会遇到与 [start, end] 区间内字符相同的情况，此时将字符作为 key 值，获取其 value 值，并更新 start，此时 [start, end] 区间内不存在重复字符
无论是否更新 start，都会更新其 map 数据结构和结果 ans。
时间复杂度：O(n)

## 代码

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length(), ans = 0;
        Map<Character, Integer> map = new HashMap<>();
        for (int end = 0, start = 0; end < n; end++) {
            char alpha = s.charAt(end);
            if (map.containsKey(alpha)) {
                start = Math.max(map.get(alpha), start);
            }
            ans = Math.max(ans, end - start + 1);
            map.put(s.charAt(end), end + 1);
        }
        return ans;
    }
}
```



```java
// 如果要输出最长子串时
public static void main(String[] args) {
        /**
         * 无重复字符的最长子串
         */
        Scanner scanner = new Scanner(System.in);
        String s = scanner.next();
        int n = s.length(), ans = 0, t = 0, v = 0;
        HashMap<Character, Integer> map = new HashMap<>();
        for (int end = 0, start = 0; end < n; end++){
            char alpha = s.charAt(end);
            if (map.containsKey(alpha)){
                start = Math.max(map.get(alpha) + 1, start);
            }
            if(ans < end - start + 1){
                t = start;
                v = end;
                ans = end - start + 1;
            }
            map.put(s.charAt(end), end);
        }
        System.out.println(s.substring(t,v+1));
    }
```

