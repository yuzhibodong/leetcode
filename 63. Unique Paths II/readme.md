# 63. Unique Paths II

## Problem
- Follow up for "Unique Paths": Now consider if some obstacles are added to the grids. How many unique paths would there be?
- An obstacle and empty space is marked as 1 and 0 respectively in the grid.

> For example,
> 
> There is one obstacle in the middle of a 3x3 grid as illustrated below.
> 
> [
>   [0,0,0],
>   
>   [0,1,0],
>   
>   [0,0,0]
>   
> ]
> 
> The total number of unique paths is 2.

- Note: m and n will be at most 100.

## Solution
- O(mn) in time & space:

```python
class Solution(object):
    def uniquePathsWithObstacles(self, obstacleGrid):
        """
        :type obstacleGrid: List[List[int]]
        :rtype: int
        """
        m, n = len(obstacleGrid), len(obstacleGrid[0])
        dp = [[0]*n for _ in range(m)]
        for i in range(m):
            if obstacleGrid[i][0] == 1: break
            dp[i][0] = 1
        for i in range(n):
            if obstacleGrid[0][i] == 1: break
            dp[0][i] = 1
        for i in range(1, m):
            for j in range(1, n):
                if obstacleGrid[i][j] == 0:
                    dp[i][j] = dp[i-1][j] + dp[i][j-1]
        return dp[-1][-1]
```

- O(mn) in time & space, shorter

```python
class Solution(object):
    def uniquePathsWithObstacles(self, obstacleGrid):
        m, n = len(obstacleGrid), len(obstacleGrid[0])
        dp = [[0]*(n+1) for _ in range(m+1)]
        dp[0][1] = 1  ##
        for i in range(1, m+1):
            for j in range(1, n+1):
                if obstacleGrid[i-1][j-1] == 0:
                    dp[i][j] = dp[i-1][j] + dp[i][j-1]
        return dp[-1][-1]
```

- O(mn) in time & O(n) in space, ref from [here](https://discuss.leetcode.com/topic/10974/short-java-solution/2)

```python
class Solution(object):
    def uniquePathsWithObstacles(self, obstacleGrid):
        m, n = len(obstacleGrid), len(obstacleGrid[0])
        dp = [0] * n  # dp[j] is the paths number to column j in the current row
        dp[0] = 1
        for row in obstacleGrid:
            for j in range(n):
                if row[j] == 1:
                    dp[j] = 0
                elif j > 0:
                    dp[j] += dp[j-1]
        return dp[-1]
```
