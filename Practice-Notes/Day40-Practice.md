# 📝 LeetCode 学习日志 Day 40

<br>

## 647. 回文子串
- 题目链接：[**LeetCode 647. Palindromic Substrings**](https://leetcode.com/problems/palindromic-substrings/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这题求的是字符串中有多少个连续的回文子串。思路是用二维 DP 判断每个区间 s[i:j+1] 是否为回文，定义 dp[i][j] 表示 s[i:j+1] 是否是回文。判断时看两端字符是否相等，如果 s[i] == s[j]，并且当前长度小于等于 2，或者中间部分 dp[i+1][j-1] 已经是回文，那么当前区间也是回文。因为 dp[i][j] 依赖下面一行的 dp[i+1][j-1]，所以 i 要倒序遍历，j 从 i 往后遍历。每发现一个回文子串，就把答案加一。


<br>

## 💻 代码实现
```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        dp = [[False] * len(s) for _ in range(len(s))]
        result = 0
        for i in range(len(s)-1, -1, -1):
            for j in range(i, len(s)):
                if s[i] == s[j] and (j-i <= 1 or dp[i+1][j-1]):
                    result += 1
                    dp[i][j] = True
        return result
```

<br>

## 516. 最长回文子序列
- 题目链接：[**LeetCode 516. Longest Palindromic Subsequence**](https://leetcode.com/problems/longest-palindromic-subsequence/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这题求的是字符串中最长的回文子序列长度，子序列不要求连续，只要保持相对顺序即可。定义 dp[i][j] 表示区间 s[i:j+1] 中最长回文子序列的长度。单个字符本身就是回文，所以初始化 dp[i][i] = 1。如果两端字符相等，说明这两个字符可以同时放进回文序列里，因此 dp[i][j] = dp[i+1][j-1] + 2；如果两端字符不相等，就不能同时选它们，只能分别尝试去掉左端或右端，取更大值，即 dp[i][j] = max(dp[i+1][j], dp[i][j-1])。同样因为依赖 i+1 这一行，所以 i 也要倒序遍历。

<br>

## 💻 代码实现
```python
class Solution:
    def longestPalindromeSubseq(self, s: str) -> int:
        dp = [[0] * len(s) for _ in range(len(s))]
        for i in range(len(s)):
            dp[i][i] = 1
        for i in range(len(s)-1, -1, -1):
            for j in range(i+1, len(s)):
                if s[i] == s[j]:
                    dp[i][j] = dp[i+1][j-1] + 2
                else:
                    dp[i][j] = max(dp[i+1][j], dp[i][j-1])
        return dp[0][-1]
```

<br>

## 📝 今日心得
今天练习的dp解决回文的问题，思路都是从后向前看，来记录最长序列是回文。