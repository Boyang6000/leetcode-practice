# 📝 LeetCode 学习日志 Day 32

<br>

## 518. 零钱兑换 II
- 题目链接：[**LeetCode 518. Coin Change II**](https://leetcode.com/problems/coin-change-ii/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题用到的是完全背包的方法。跟01背包不同的是完全背包是正序，不是倒序，因为每一个数字可以无限用。这道题求的是组合数，所以两层循环的外循环是硬币种类，内循环是amount，这样不会把不同顺序都算进去。

<br>

## 💻 代码实现
```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        dp = [0] * (amount + 1)
        dp[0] = 1
        for i in range(len(coins)):
            for j in range(coins[i], amount + 1):
                dp[j] += dp[j - coins[i]]
        return dp[amount] 
```

<br>

## 377. 组合总和 IV
- 题目链接：[**LeetCode 377. Combination Sum IV**](https://leetcode.com/problems/combination-sum-iv/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题跟477的区别在于是求的排列数，顺序不同也算一种方法，所以外循环target内循环数字。

<br>

## 💻 代码实现
```python
class Solution:
    def combinationSum4(self, nums: List[int], target: int) -> int:
        dp = [0] * (target + 1)
        dp[0] = 1
        for i in range(1, target + 1):
            for j in range(len(nums)):
                if i - nums[j] >= 0:
                    dp[i] += dp[i-nums[j]]  
        return dp[target]
```

<br>

## 📝 今日心得
今天做的是完全背包的内容，完全背包跟01背包的不同在于一样物品可以无限次的去选。完全背包分为两种情况，一种是求组合数一种是求排列数，不同的点在于顺序不同是算相同还是算不同。