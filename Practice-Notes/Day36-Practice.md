# 📝 LeetCode 学习日志 Day 35

<br>

## 121. 买卖股票的最佳时机
- 题目链接：[**LeetCode 121. Best Time to Buy and Sell Stock**](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题用到的是动态规划的方法，dp0记录的是手里持股的状态，dp1记录的是手里不持股的状态


<br>

## 💻 代码实现
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        dp0, dp1 = -prices[0], 0
        for i in range(1, len(prices)):
            dp1 = max(dp1, dp0 + prices[i])
            dp0 = max(dp0, -prices[i])
        return dp1
```

<br>

## 122. 买卖股票的最佳时机 II
- 题目链接：[**LeetCode 122. Best Time to Buy and Sell Stock II**](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
在121的基础上，因为可以多次买入卖出，今天不持有的话，可以用之前的利润来买入，所以dp0需要改动。

<br>

## 💻 代码实现
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        dp = [[0] * 2 for _ in range(len(prices))]
        dp[0][0] = -prices[0]
        dp[0][1] = 0
        for i in range(1, len(prices)):
            dp[i][0] = max(dp[i-1][0], dp[i-1][1] - prices[i])
            dp[i][1] = max(dp[i-1][1], dp[i-1][0] + prices[i])
        return dp[-1][1]
```

<br>

## 123. 买卖股票的最佳时机 III
- 题目链接：[**LeetCode 123. Best Time to Buy and Sell Stock III**](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
在120，121的基础上，因为只能买卖两次，所以一天一共就有五个状态：
1. 没有操作
2. 第一次持有股票
3. 第一次不持有股票
4. 第二次持有股票
5. 第二次不持有股票

<br>

## 💻 代码实现
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if len(prices) == 0:
            return 0
        dp = [0] * 5
        dp[1] = -prices[0]
        dp[3] = -prices[0]
        for i in range(1, len(prices)):
            dp[1] = max(dp[1], dp[0] - prices[i])
            dp[2] = max(dp[2], dp[1] + prices[i])
            dp[3] = max(dp[3], dp[2] - prices[i])
            dp[4] = max(dp[4], dp[3] + prices[i])
        return dp[4]
```

<br>

## 📝 今日心得
今天练习的的是股票买卖的三种变化，一种是只能买卖一次，一种是买卖多次，一种是买卖两次，重点在于记录每一天的不同状态。