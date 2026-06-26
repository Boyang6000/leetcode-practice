# 📝 LeetCode 学习日志 Day 36

<br>

## 188. 买卖股票的最佳时机 IV
- 题目链接：[**LeetCode 188. Best Time to Buy and Sell Stock IV**](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题是123的泛化，偶数为买入/持股，奇数为卖出


<br>

## 💻 代码实现
```python
class Solution:
    def maxProfit(self, k: int, prices: List[int]) -> int:
        dp = [0] * k * 2
        for i in range(k):
            dp[i * 2] = -prices[0]
        for price in prices[1:]:
            dc = dp[:]
            for i in range(2 * k):
                if i % 2 == 1:
                    dp[i] = max(dc[i], dc[i-1] + price)
                else:
                    pre = 0 if i == 0 else dc[i-1]
                    dp[i] = max(dc[i], pre - price)
        return dp[-1]
```

<br>

## 309. 最佳买卖股票时机含冷冻期
- 题目链接：[**LeetCode 309. Best Time to Buy and Sell Stock with Cooldown**](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
在123的基础上，分成四种状态：dp[0] = hold，dp[1] = free，dp[2] = sold，dp[3] = cooldown

<br>

## 💻 代码实现
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        dp = [-prices[0], 0, 0, 0]
        for price in prices[1:]:
            dc = dp[:]
            dp[0] = max(dc[0], dc[1] - price, dc[3] - price)
            dp[1] = max(dc[1], dc[3])
            dp[2] = dc[0] + price
            dp[3] = dc[2]
        return max(dp)
```

<br>

## 714. 买卖股票的最佳时机含手续费
- 题目链接：[**LeetCode 714. Best Time to Buy with Transaction Fee**](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
在123的基础上，记录两个状态，一个是holding，一个是not holding。

<br>

## 💻 代码实现
```python
class Solution:
    def maxProfit(self, prices: List[int], fee: int) -> int:
        dp = [0] * 2
        dp[0] = -prices[0] - fee
        for price in prices:
            dp[0] = max(dp[0], dp[1] - price - fee)
            dp[1] = max(dp[1], dp[0] + price)
        return max(dp)
```

<br>

## 📝 今日心得
今天练习的的是股票买卖的几种变化，重点在于用dp来去记录不同的状态，update状态看保持max保持这种状态还是从别的状态变成记录的这个状态。