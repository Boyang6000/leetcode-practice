# 📝 LeetCode 学习日志 Day 35

<br>

## 416. 分割等和子集
- 题目链接：[**LeetCode 416. Partition Equal Subset Sum**](https://leetcode.com/problems/partition-equal-subset-sum/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题用到的是01背包的方法，首先先判断sum是否能被2整除。然后将sum的一半看作是背包的容量，数字看作是物品的价值和重量，是一样的等同于这个数字。当背包被塞满时，查看背包的价值是否等于sum的一半。

这道题用的是一维数组来实现01背包的。在这个一维数组中，初始化都为0，然后需要两次循环，第一次是对于每个物品的循环，是正循环，第二次是对背包容量的一个循环，这里采用的是倒序，为了避免多次添加同个物品。


<br>

## 💻 代码实现
```java
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for(int i: nums){
            sum += i;
        }
        if(sum % 2 == 1) return false;
        int half = sum / 2;

        int[] dp = new int[half + 1];
        for(int i = 0; i < nums.length; i++){
            for(int j = half; j >= nums[i]; j--){
                dp[j] = Math.max(dp[j], dp[j - nums[i]] + nums[i]);
            }
        }    

        return dp[half] == half;
    }
}
```

<br>

## 📝 今日心得
背包问题非常的深奥，里面的变化也是特别多的。今天认真学习了01背包的二维数组实现和一维数组的实现。因为二维数组的公式推导是由左上的值和上方的值进行推导，压缩到一维数组里可以理解为复制了上方的数组，然后再和左上的值进行推导，这里的重点在于背包容量循环是倒序，如果是正序的话，物品会被添加多次，导致数据不准确。