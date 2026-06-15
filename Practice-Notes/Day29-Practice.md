# 📝 LeetCode 学习日志 Day 34

<br>

## 62. 不同路径
- 题目链接：[**LeetCode 62. Unique Paths**](https://leetcode.com/problems/unique-paths/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
要从结果来倒推公式。

想要求dp[i][j]，只能有两个方向来推导出来，即dp[i - 1][j] 和 dp[i][j - 1]。

此时在回顾一下 dp[i - 1][j] 表示啥，是从(0, 0)的位置到(i - 1, j)有几条路径，dp[i][j - 1]同理。

那么很自然，**dp[i][j] = dp[i - 1][j] + dp[i][j - 1]**，因为dp[i][j]只有这两个方向过来。

<br>

## 💻 代码实现
```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        for (int i = 0; i < m; i++) dp[i][0] = 1;
        for (int j = 0; j < n; j++) dp[0][j] = 1;
        for(int k = 1; k < m; k++){
            for(int l = 1; l < n; l++){
                dp[k][l] = dp[k-1][l] + dp[k][l-1];
            }
        }
        return dp[m-1][n-1];
    }
}
```

<br>

## 63. 不同路径 II
- 题目链接：[**LeetCode 63. Unique Paths II**](https://leetcode.com/problems/unique-paths-ii/)
- 关键词：**Dynamic Programming**

<br>

## 💡 思路
这道题其实跟62是一样的。只不过需要加一个对于障碍的处理，障碍上的路径为0。

还有需要对边界值进行处理，如果起始点和终点是障碍，直接为0。

初始设定时，如果边上有障碍的话，也是为0。


<br>

## 💻 代码实现
```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[][] dp = new int[m][n];
        if (obstacleGrid[m - 1][n - 1] == 1 || obstacleGrid[0][0] == 1) {
            return 0;
        }
        for (int i = 0; i < m && obstacleGrid[i][0] == 0; i++) dp[i][0] = 1;
        for (int j = 0; j < n && obstacleGrid[0][j] == 0; j++) dp[0][j] = 1;
        for(int k = 1; k < m; k++){
            for(int l = 1; l < n; l++){
                if(obstacleGrid[k][l] == 0){
                    dp[k][l] = dp[k-1][l] + dp[k][l-1];
                }
                else{
                    dp[k][l] = 0;
                }
            }
        }
        return dp[m-1][n-1];
    }
}
```

<br>

## 📝 今日心得
相对而言，dp的感觉还是简单一些，主要考虑好起始的值以及每一层递归公式的逻辑就行。