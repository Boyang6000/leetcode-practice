# 📝 LeetCode 学习日志 Day 39

<br>

## 115. 不同的子序列
- 题目链接：[**LeetCode 115. Distinct Subsequences**](https://leetcode.com/problems/distinct-subsequences/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题用的是dp的思路，当s[i-1] == t[j-1]时，我们可以用s[i-1]去匹配t[j-1]，也可以用s[:i-1]去匹配t[:j]


<br>

## 💻 代码实现
```python
class Solution:
    def numDistinct(self, s: str, t: str) -> int:
        dp = [[0]*(len(t)+1) for _ in range(len(s)+1)]
        for i in range(len(s)):
            dp[i][0] = 1
        for j in range(1, len(t)):
            dp[0][j] = 0
        for i in range(1, len(s)+1):
            for j in range(1, len(t)+1):
                if s[i-1] == t[j-1]:
                    dp[i][j] = dp[i-1][j-1] + dp[i-1][j]
                else:
                    dp[i][j] = dp[i-1][j]
        return dp[-1][-1]
```

<br>

## 583. 两个字符串的删除操作
- 题目链接：[**LeetCode 583. Delete Opration for Two Strings**](https://leetcode.com/problems/delete-operation-for-two-strings/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题跟115其实很像，两个词相等的时候就不用删除，不相等的时候看哪种删除方式花费最少

<br>

## 💻 代码实现
```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        dp = [[0]*(len(word2)+1) for _ in range(len(word1)+1)]
        for i in range(len(word1)+1):
            dp[i][0] = i
        for j in range(len(word2)+1):
            dp[0][j] = j
        for i in range(1, len(word1)+1):
            for j in range(1, len(word2)+1):
                if word1[i-1] == word2[j-1]:
                    dp[i][j] = dp[i-1][j-1]
                else:
                    dp[i][j] = min(dp[i-1][j-1]+2, dp[i-1][j] + 1, dp[i][j-1]+1)
        return dp[-1][-1] 
```

<br>

## 72. 编辑距离
- 题目链接：[**LeetCode 72. Edit Distance**](https://leetcode.com/problems/maximum-length-of-repeated-subarray/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
在583的基础上把花费改成1

<br>

## 💻 代码实现
```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        dp = [[0]*(len(word2)+1) for _ in range(len(word1)+1)]
        for i in range(len(word1)+1):
            dp[i][0] = i
        for j in range(len(word2)+1):
            dp[0][j] = j
        for i in range(1, len(word1)+1):
            for j in range(1, len(word2)+1):
                if word1[i-1] == word2[j-1]:
                    dp[i][j] = dp[i-1][j-1]
                else:
                    dp[i][j] = min(dp[i-1][j-1]+1, dp[i-1][j] + 1, dp[i][j-1]+1)
        return dp[-1][-1] 
```

<br>

## 📝 今日心得
这个系列就是编辑距离的几种变化，重点在于看两个字符相等时怎么操作，不相等时怎么操作