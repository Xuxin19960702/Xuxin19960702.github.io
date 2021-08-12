---
title: 数字流的秩
date: 2021-08-12 19:57:00
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

假设你正在读取一串整数。每隔一段时间，你希望能找出数字 x 的秩(小于或等于 x 的值的个数)。请实现数据结构和算法来支持这些操作，也就是说：

实现 track(int x) 方法，每读入一个数字都会调用该方法；

实现 getRankOfNumber(int x) 方法，返回小于或等于 x 的值的个数。

## 示例

> 输入：["StreamRank", "getRankOfNumber", "track", "getRankOfNumber"]
>            [[], [1], [0], [0]]
>
> 输出：[null,0,null,1]
>

<!--more-->

## 限制

- `x <= 50000`
- `track` 和 `getRankOfNumber` 方法的调用次数均不超过 2000 次

## 思路

## 代码

```java
class StreamRank {
    List<Integer> list;
    public StreamRank() {
            list=new ArrayList<>();
    }
    
    public void track(int x) {
        list.add(x);
    }
    
    public int getRankOfNumber(int x) {
        int res=0;
        if(list.size() != 0){
            for(int i=0;i<list.size();i++){
                if(list.get(i) <= x){
                        res++;
                }
            }
            return res;
        }
        return 0;
        
    }
}
```



