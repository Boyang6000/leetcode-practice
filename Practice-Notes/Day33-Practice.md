# 📝 LeetCode 学习日志 Day 33

<br>

## 322. 零钱兑换
- 题目链接：[**LeetCode 322. Coin Change**](https://leetcode.com/problems/coin-change/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题用到的是完全背包的方法，因为求的是最少硬币数量，所以组合数还是排列数都可以。


<br>

## 💻 代码实现
```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [float('inf')] * (amount + 1)
        dp[0] = 0
        for i in range(1, amount + 1):
            for coin in coins:
                if i - coin >= 0:
                    dp[i] = min(dp[i], dp[i-coin] + 1)
        return dp[amount] if dp[amount] != float('inf') else -1
```

<br>

## 279. 完全平方数
- 题目链接：[**LeetCode 279. Perfect Squares**](https://leetcode.com/problems/perfect-squares/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题也是用的完全背包，背包容量为n，物品为完全平方数。

<br>

## 💻 代码实现
```python
class Solution:
    def numSquares(self, n: int) -> int:
        dp = [float('inf')] * (n+1)
        dp[0] = 0

        for i in range(1, n+1):
            for j in range(1, int(i**0.5) + 1):
                dp[i] = min(dp[i], dp[i - j*j] + 1)
        return dp[n]
```

<br>

## 139. 单词拆分
- 题目链接：[**LeetCode 139. Word Break**](https://leetcode.com/problems/word-break/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题用的是完全背包，s是背包，wordDict是物品。

<br>

## 💻 代码实现
```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        dp = [False] * (len(s) + 1)
        dp[0] = True
        for j in range(1, len(s) + 1):
            for word in wordDict:
                if j >= len(word):
                    dp[j] = dp[j] or (dp[j-len(word)] and word == s[j-len(word):j])
        return dp[len(s)]
```

<br>

## 📝 今日心得
今天练习的还是完全背包，主要的点在于怎么把问题抽象成背包问题，分清楚背包容量和物品价值分别是什么，然后更新每个背包的方式是什么。