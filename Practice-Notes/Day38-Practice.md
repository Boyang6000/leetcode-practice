# 📝 LeetCode 学习日志 Day 38

<br>

## 1143. 最长公共子序列
- 题目链接：[**LeetCode 1143. Longest Common Subsequence**](https://leetcode.com/problems/longest-common-subsequence/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题也是用dp来去做，分两种情况，一种是text1[i] == text2[i], 那么dp[i][j] == dp[i-1][j-1] + 1；如果text1[i] != text2[i]，那么dp[i][j] = max(dp[i-1][j], dp[i][j-1])


<br>

## 💻 代码实现
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m, n = len(text1), len(text2)
        dp = [0] * (n+1)
        for i in range(1, m+1):
            prev = 0
            for j in range(1, n+1):
                curr = dp[j]
                if text1[i-1] == text2[j-1]:
                    dp[j] = prev + 1
                else:
                    dp[j] = max(dp[j], dp[j-1])
                prev = curr
        return dp[n]
```

<br>

## 1035. 不相交的线
- 题目链接：[**LeetCode 1035. Uncrossed Lines**](https://leetcode.com/problems/uncrossed-lines/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这个其实就是1143最长公共子序列，因为相对顺序不变的话，相连接的线就不会相交

<br>

## 💻 代码实现
```python
class Solution:
    def maxUncrossedLines(self, nums1: List[int], nums2: List[int]) -> int:
        dp = [[0] * (len(nums2)+1) for _ in range(len(nums1) + 1)]
        for i in range(1, len(nums1) + 1):
            for j in range(1, len(nums2) + 1):
                if nums1[i-1] == nums2[j-1]:
                    dp[i][j] = dp[i-1][j-1] + 1
                else:
                    dp[i][j] = max(dp[i-1][j], dp[i][j-1])
        return dp[-1][-1]
```

<br>

## 53. 最大子序和
- 题目链接：[**LeetCode 53. Maximum Subarray**](https://leetcode.com/problems/maximum-subarray/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题用的是一维dp的解法，dp[i] 就是以 nums[i] 结尾的最大连续子数组和，那么只有两种情况，要么是把nums[i]加入到前面最大的序列里面，要么就是以nums[i]重新开始序列

<br>

## 💻 代码实现
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        dp = [0] * len(nums)
        dp[0] = nums[0]
        result = dp[0]
        for i in range(1, len(nums)):
            dp[i] = max(nums[i], dp[i-1] + nums[i])
            result = max(result, dp[i])
        return result
```

<br>

## 392. 判断子序和
- 题目链接：[**LeetCode 392. Is Subsequence**](https://leetcode.com/problems/is-subsequence/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题跟判断最长公共子序列是一样的，只要看最后数字是不是等于目标字符串长度就可以。

<br>

## 💻 代码实现
```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        dp = [[0]*(len(t) + 1) for _ in range(len(s)+1)]
        for i in range(1, len(s) + 1):
            for j in range(1, len(t) + 1):
                if s[i-1] == t[j-1]:
                    dp[i][j] = dp[i-1][j-1] + 1
                else:
                    dp[i][j] = max(dp[i-1][j], dp[i][j-1])
        return dp[-1][-1] == len(s)
```

<br>

## 📝 今日心得
今天练习的题目都是跟最长公共子序列相关的，重点在于分成两类，一种是text1[i] == text2[i], 那么dp[i][j] == dp[i-1][j-1] + 1；如果text1[i] != text2[i]，那么dp[i][j] = max(dp[i-1][j], dp[i][j-1])