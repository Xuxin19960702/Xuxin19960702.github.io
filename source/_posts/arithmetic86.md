---
title: 扁平化嵌套列表迭代器
date: 2021-08-10 17:37:00
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

给你一个嵌套的整数列表 nestedList 。每个元素要么是一个整数，要么是一个列表；该列表的元素也可能是整数或者是其他列表。请你实现一个迭代器将其扁平化，使之能够遍历这个列表中的所有整数。

实现扁平迭代器类 NestedIterator ：

- NestedIterator(List<NestedInteger> nestedList) 用嵌套列表 nestedList 初始化迭代器。
- int next() 返回嵌套列表的下一个整数。
- boolean hasNext() 如果仍然存在待迭代的整数，返回 true ；否则，返回 false 。

如果 `res` 与预期的扁平化列表匹配，那么你的代码将会被判为正确。

## 示例

> 输入：nestedList = [[1,1],2,[1,1]]
>
> 输出：[1,1,2,1,1]
>
> 解释：通过重复调用 next 直到 hasNext 返回 false，next 返回的元素的顺序应该是: [1,1,2,1,1]。

<!--more-->

## 限制

- `1 <= nestedList.length <= 500`
- 嵌套列表中的整数值在范围 `[-106, 106]` 内

## 思路

嵌套的整型列表是一个树形结构，树上的叶子节点对应一个整数，非叶节点对应一个列表。

在这棵树上深度优先搜索的顺序就是迭代器遍历的顺序。

我们可以先遍历整个嵌套列表，将所有整数存入一个数组，然后遍历该数组从而实现 next 和 hasNext 方法。

## 代码

```java
public class NestedIterator implements Iterator<Integer> {
    private List<Integer> vals;
    private Iterator<Integer> cur;

    public NestedIterator(List<NestedInteger> nestedList) {
        vals = new ArrayList<Integer>();
        dfs(nestedList);
        cur = vals.iterator();
    }

    @Override
    public Integer next() {
        return cur.next();
    }

    @Override
    public boolean hasNext() {
        return cur.hasNext();
    }

    private void dfs(List<NestedInteger> nestedList) {
        for (NestedInteger nest : nestedList) {
            if (nest.isInteger()) {
                vals.add(nest.getInteger());
            } else {
                dfs(nest.getList());
            }
        }
    }
}
```



