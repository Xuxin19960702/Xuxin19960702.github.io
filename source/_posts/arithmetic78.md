---
title: 剑指 Offer II 112. 最长递增路径
date: 2021-08-05 15:44:00
categories: 算法题
archives:
tags: [Java,算法]
---

## 题目

给定一个 m x n 整数矩阵 matrix ，找出其中 **最长递增路径** 的长度。

对于每个单元格，你可以往上，下，左，右四个方向移动。 **不能** 在 **对角线** 方向上移动或移动到 **边界外**（即不允许环绕）。

## 示例

> 输入：matrix = [[9,9,4],[6,6,8],[2,1,1]]
>
> 输出： 4
>
> 解释：最长递增路径为 [1, 2, 6, 9]。

<!--more-->

![](/arithmetic78/grid1.jpg)

## 限制

- m == matrix.length
- n == matrix[i].length
- 1 <= m, n <= 200
- 0 <= matrix[i][j] <= 231 - 1

## 思路

1. 总体框架为图的深度搜索，遍历矩阵中的每个节点，进行满足递增的深度搜索。
2. 暴力解法，在第135个case的时候会超时，这个时候引入记忆化搜索，每次搜索的时候，可以去判断这个节点之前有没有搜索过，如果搜索过，则使用之前保存的值

## 代码

```java
class Solution {
    public int longestIncreasingPath(int[][] grid) {
        int rowSize = grid.length;
        int colSize = grid[0].length;
        int lastMax = 0;
        int[][] has = new int[rowSize][colSize];
        int[][] dp = new int[rowSize][colSize];
        for(int i=0;i<rowSize;i++){
            for(int j=0;j<colSize;j++){
                int len = dfs(grid,i,j,has,dp);
                dp[i][j] = len;
                lastMax = Math.max(len,lastMax);
            }
        }
        return lastMax;
    }

    private static int dfs(int[][] grid,int row,int col,int[][] has,int[][] dp){
        if(has[row][col] == 1){
            return 0 ;
        }
        if(dp[row][col] > 0){
            return dp[row][col];
        }
        int rowSize = grid.length;
        int colSize = grid[0].length;

        int current = grid[row][col];
        has[row][col] = 1;
        int size = 0;
        if(row-1 >= 0 && grid[row-1][col] > current){
            int res = dfs(grid,row-1,col,has,dp);
            size = Math.max(size,res);
        }

        if(row+1 < rowSize && grid[row+1][col] > current){
            int res = dfs(grid,row+1,col,has,dp);
            size = Math.max(size,res);
        }

        if(col-1 >= 0 && grid[row][col-1] > current){
            int res = dfs(grid,row,col-1,has,dp);
            size = Math.max(size,res);
        }

        if(col+1 < colSize && grid[row][col+1] > current){
            int res = dfs(grid,row,col+1,has,dp);
            size = Math.max(size,res);
        }
        dp[row][col] = Math.max(size+1,dp[row][col]);
        has[row][col] = 0;
        return size+1;
    }
}
```



