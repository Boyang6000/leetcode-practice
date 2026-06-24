# 📝 LeetCode 学习日志 Day 35

<br>

## 198. 打家劫舍
- 题目链接：[**LeetCode 198. House Robber**](https://leetcode.com/problems/house-robber/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题用到的是动态规划的方法，因为抢不抢这个房子的钱取决于之前的房子有没有被抢，所以用dp来解决。


<br>

## 💻 代码实现
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if not nums:
            return 0
        prev_max = 0
        cur_max = 0

        for num in nums:
            temp = cur_max
            cur_max = max(prev_max + num, cur_max)
            prev_max = temp
        return cur_max
```

<br>

## 213. 打家劫舍 II
- 题目链接：[**LeetCode 213. House Robber II**](https://leetcode.com/problems/house-robber-ii/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题用的是198的思路，因为现在房子变成环了，所以要考虑三种情况：一是首尾都不考虑，二是不考虑首个房子，三是不考虑尾部的房子，因为二三包括一了，所以只需要把二三的结果算出来取最大的那个就行了。

<br>

## 💻 代码实现
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if not nums:
            return 0
        
        if len(nums) == 1:
            return nums[0]

        prev_max = 0
        res1 = 0
        for num in nums[1:]:
            temp = res1
            res1 = max(prev_max + num, res1)
            prev_max = temp
        
        prev_max = 0
        res2 = 0
        for num in nums[:-1]:
            temp = res2
            res2 = max(prev_max + num, res2)
            prev_max = temp

        return max(res1, res2)
```

<br>

## 337. 打家劫舍 III
- 题目链接：[**LeetCode 337. House Robber III**](https://leetcode.com/problems/house-robber-iii/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题就是经典的树形dp的写法，分成两个状态，一个是偷当前node的最大值，一个是不偷当前node的最大值，然后通过递归来update。
递归的关键点在于，偷不偷当前node取决于是否偷他的左右child，所以必须要先递归到底部，再一步步算上来，也就是后序遍历。

<br>

## 💻 代码实现
```python
class Solution:
    def rob(self, root: Optional[TreeNode]) -> int:
        dp = self.traverse(root)
        return max(dp)

    def traverse(self, node):
        if not node:
            return (0, 0)
        left = self.traverse(node.left)
        right = self.traverse(node.right)

        val_0 = max(left[0], left[1]) + max(right[0], right[1])
        val_1 = node.val + left[0] + right[0]
        return (val_0, val_1)
```

<br>

## 📝 今日心得
今天练习的的是三种不同的dp写法，第一种是线形dp，第二种是环形dp，第三种是树形dp，都是非常经典的。