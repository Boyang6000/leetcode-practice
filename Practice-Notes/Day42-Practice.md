# 📝 LeetCode 学习日志 Day 42

<br>

## 98. 所有可达路径
- 题目链接：[**LeetCode 98. Trapping Rain Water**](https://leetcode.com/problems/trapping-rain-water/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题是非常经典的面试题，利用单调栈可以来解决。当当前height比stack末尾的height还大时，看stack里面是否有左边界，如果有左边界则可以接雨水。


<br>

## 💻 代码实现
```python
class Solution:
    def trap(self, height: List[int]) -> int:
        stack = [0]
        result = 0
        for i in range(1, len(height)):
            while stack and height[i] > height[stack[-1]]:
                mid_height = stack.pop()
                if stack:
                    h = min(height[stack[-1]], height[i]) - height[mid_height]
                    w = i - stack[-1] -1
                    result += h * w
            stack.append(i)
        return result
```

<br>

## 📝 今日心得
今天练习的是单调栈的两道经典面试题，第一次接触单调栈还是会觉得有一些抽象，看是找两边比中间高还是两边比中间矮来确定单调栈递增还是递减。