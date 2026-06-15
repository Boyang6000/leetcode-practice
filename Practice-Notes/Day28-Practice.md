# 📝 LeetCode 学习日志 Day 32

<br>

## 509. 斐波那契数
- 题目链接：[**LeetCode 509. Fibonacci Number**](https://leetcode.com/problems/fibonacci-number/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题是dp里面最基础的一道题。

**动规五部曲：**

这里我们要用一个一维dp数组来保存递归的结果

 - 确定dp数组以及下标的含义：

     - **dp[i]的定义为：第i个数的斐波那契数值是dp[i]**

 - 确定递推公式
     - 为什么这是一道非常简单的入门题目呢？因为题目已经把递推公式直接给我们了：**状态转移方程 dp[i] = dp[i - 1] + dp[i - 2];**

 - dp数组如何初始化
     - **dp[0] = 0; dp[1] = 1;**
 
 - 确定遍历顺序
     - 从递归公式dp[i] = dp[i - 1] + dp[i - 2];中可以看出，dp[i]是依赖 dp[i - 1] 和 dp[i - 2]，那么遍历的顺序一定是**从前到后**遍历的

 - 举例推导dp数组
     - 按照这个递推公式dp[i] = dp[i - 1] + dp[i - 2]，我们来推导一下，当N为10的时候，dp数组应该是如下的数列：

        0 1 1 2 3 5 8 13 21 34 55

<br>

## 💻 代码实现
```java
class Solution {
    public int fib(int n) {
        if(n <= 1) return n;
        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;
        for(int index = 2; index <= n; index++){
            dp[index] = dp[index - 1] + dp[index - 2];
        }
        return dp[n];
    }
}
```

<br>

## 70. 爬楼梯
- 题目链接：[**LeetCode 70. Climbing Stairs**](https://leetcode.com/problems/climbing-stairs/)
- 关键词：**Dynamic Programming**

<br>

## 💡 思路
这道题其实跟509是一样的。

第一层有1种方法，第二层有2种方法，第三层可以通过第一层走一步或两步，或者第二层走一步来实现，说明第三层的方法跟第一二层是相关的。


<br>

## 💻 代码实现
```java
class Solution {
    public int climbStairs(int n) {
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 1;
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
}
```

<br>

## 746. 使用最小花费爬楼梯
- 题目链接：[**LeetCode 746. Min Cost Climbing Stairs**](https://leetcode.com/problems/min-cost-climbing-stairs/)
- 关键词：**Dynamic Programming**

<br>

## 💡 思路
这道题其实跟70是一样的。只需要增加一个cost的比较。


<br>

## 💻 代码实现
```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int len = cost.length;
        int[] dp = new int[len + 1];

        dp[0] = 0;
        dp[1] = 0;

        for(int i = 2; i <= len; i++){
            dp[i] = Math.min(dp[i-1] + cost[i-1], dp[i-2] + cost[i-2]);
        }

        return dp[len];
    }
}
```

<br>

## 📝 今日心得
相对而言，dp的感觉还是简单一些，主要考虑好起始的值以及每一层递归公式的逻辑就行。