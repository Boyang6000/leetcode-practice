# 📝 LeetCode 学习日志 Day 37

<br>

## 300. 最长递增子序列
- 题目链接：[**LeetCode 300. Longest Increasing Subsequence**](https://leetcode.com/problems/longest-increasing-subsequence/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题是dp解决子序列的一个例题，用dp[i]来记录以nums[i]为结尾的最长子序列是多少，然后如果nums[i] > nums[j]，说明nums[i]可以接在nums[j]后面，那么就比较dp[i] 跟dp[j] + 1哪个大就保存哪个。


<br>

## 💻 代码实现
```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        if len(nums) <= 1:
            return len(nums)
        dp = [1] * len(nums)
        result = 1
        for i in range(1, len(nums)):
            for j in range(0, i):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i], dp[j] + 1)
            result = max(result, dp[i])
        return result
```

<br>

## 674. 最长连续递增序列
- 题目链接：[**LeetCode 674. Longest Continuous Increasing Subsequence**](https://leetcode.com/problems/longest-continuous-increasing-subsequence/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这个就是在300的基础上，加了一个连续的设定。

<br>

## 💻 代码实现
```python
class Solution:
    def findLengthOfLCIS(self, nums: List[int]) -> int:
        if len(nums) <= 1:
            return len(nums)
        dp = [1] * len(nums)
        result = 1
        for i in range(1, len(nums)):
            if nums[i] > nums[i-1]:
                dp[i] = dp[i-1] + 1
            result = max(result, dp[i])
        return result
```

<br>

## 718. 最长重复子数组
- 题目链接：[**LeetCode 718. Maximum Length of Repeated Subarray**](https://leetcode.com/problems/maximum-length-of-repeated-subarray/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题用的是二维dp的解法，也是用dp记录以当前数字为结尾的最大序列，但是重点在于dp[i][j] = dp[i-1][j-1] + 1，说明增长是从左上角来的，所以在设定dp和循环range的时候，得多一位。

<br>

## 💻 代码实现
```python
class Solution:
    def findLength(self, nums1: List[int], nums2: List[int]) -> int:
        dp = [[0] * (len(nums2)+1) for _ in range(len(nums1)+1)]
        result = 0
        for i in range(1, len(nums1) + 1):
            for j in range(1, len(nums2) + 1):
                if nums1[i-1] == nums2[j-1]:
                    dp[i][j] = dp[i-1][j-1] + 1
                if dp[i][j] > result:
                    result = dp[i][j]
        return result
```

<br>

## 📝 今日心得
今天练习的dp解决增长序列的问题，一个全新的思路就是用dp来记录以当前数字为结尾的最大增长序列。