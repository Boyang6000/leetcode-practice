# 📝 LeetCode 学习日志 Day 31

<br>

## 1049. 最后一块石头的重量 II
- 题目链接：[**LeetCode 1049. Last Stone Weight II**](https://leetcode.com/problems/last-stone-weight-ii/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题用到的是01背包的方法，跟416是一样的，将这堆石头分成两个相同的重量，那他们互相相撞的结果就是剩下最小的重量了。

那么就是看最多能装多少重量，设定背包容量为总重量的一半。


<br>

## 💻 代码实现
```java
class Solution {
    public int lastStoneWeightII(int[] stones) {
        int sum = 0;
        for(int stone: stones){
            sum += stone;
        }
        int target = sum >> 1;

        int[] dp = new int[target + 1];
        for(int i = 0; i < stones.length; i++){
            for(int j = target; j >= stones[i]; j--){
                dp[j] = Math.max(dp[j], dp[j - stones[i]] + stones[i]);
            }
        }

        return sum - 2*dp[target];
    }
}
```

```python
class Solution:
    def lastStoneWeightII(self, stones: List[int]) -> int:
        total = sum(stones)
        target = total // 2
        dp = [0] * (target + 1)
        for i in stones:
            for j in range(target, i - 1, -1):
                dp[j] = max(dp[j], dp[j-i] + i)
        
        return total - 2*dp[-1]
```

<br>

## 494. 目标和
- 题目链接：[**LeetCode 494. Target Sum**](https://leetcode.com/problems/target-sum/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题用到的是01背包的方法。首先思考怎么将这道题放进01背包问题的框架里，

设定加法的部分和为x，减法部分的和为y，那么sum就等于x + y， target就等于x - y，那么 x = （sum + target）/ 2，我们只要找出哪些为x就行

那么背包的容量就为x，找到符合x的个数就行。

<br>

## 💻 代码实现
```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        int sum = 0;
        for(int i = 0; i < nums.length; i++){
            sum += nums[i];
        }

        if(Math.abs(target) > sum) return 0;
        if((target + sum) % 2 == 1) return 0;

        int size = (target + sum) / 2;
        int[] dp = new int[size + 1];
        dp[0] = 1;
        for(int i = 0; i < nums.length; i++){
            for(int j = size; j >= nums[i]; j--){
                dp[j] += dp[j-nums[i]];
            }
        }

        return dp[size];
    }
}
```

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        total = sum(nums)
        if abs(target) > total:
            return 0
        if (target + total) % 2 == 1:
            return 0
        target_sum = (target + total) // 2
        dp = [0] * (target_sum + 1)
        dp[0] = 1
        for num in nums:
            for i in range(target_sum, num - 1, -1):
                dp[i] += dp[i-num]
        return dp[target_sum]
```

<br>

## 474. 目标和
- 题目链接：[**LeetCode 474. Ones and Zeroes**](https://leetcode.com/problems/ones-and-zeroes/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题本质上还是用到的是01背包的方法。这个是二维01背包，两个维度，m和n

<br>

## 💻 代码实现
```python
class Solution:
    def findMaxForm(self, strs: List[str], m: int, n: int) -> int:
        dp = [[0] * (n + 1) for _ in range(m + 1)]
        for s in strs:
            zeroNum = s.count('0')
            oneNum = len(s) - zeroNum
            for i in range(m, zeroNum - 1, -1):
                for j in range(n, oneNum - 1, -1):
                    dp[i][j] = max(dp[i][j], dp[i-zeroNum][j-oneNum] + 1)
        return dp[m][n]
```

<br>

## 📝 今日心得
背包问题非常的深奥，里面的变化也是特别多的。今天认真学习了01背包的二维数组实现和一维数组的实现。因为二维数组的公式推导是由左上的值和上方的值进行推导，压缩到一维数组里可以理解为复制了上方的数组，然后再和左上的值进行推导，这里的重点在于背包容量循环是倒序，如果是正序的话，物品会被添加多次，导致数据不准确。