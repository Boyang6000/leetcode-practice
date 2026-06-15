# 📝 LeetCode 学习日志 Day 26

<br>

## 452. 用最少数量的箭引爆气球
- 题目链接：[**LeetCode 452. Minimum Number of Arrows to Burst Balloons**](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/)
- 关键词：**Greedy**  

<br>

## 💡 思路
这道题采用了贪心算法。当两个区域有重叠时，可以通过一只箭射掉两个气球。

当两个区域不重叠时，需要多一根箭；当两个区域重叠时，将当前区域的末尾调整成重叠末尾。

<br>

## 💻 代码实现
```java
class Solution {
    public int findMinArrowShots(int[][] points) {
        Arrays.sort(points, (a, b) -> Integer.compare(a[0], b[0]));

        int count = 1;
        for(int i = 1; i < points.length; i++){
            if(points[i][0] > points[i-1][1]){
                count++;
            }
            else{
                points[i][1] = Math.min(points[i][1], points[i-1][1]);
            }
        }
        return count;
    }
}
```

<br>

## 435. 无重叠区间
- 题目链接：[**LeetCode 435. Non-overlapping Intervals**](https://leetcode.com/problems/non-overlapping-intervals/)
- 关键词：**Greedy**

<br>

## 💡 思路
这道题采用的是贪心算法，跟452类似，只要减去箭的个数就是不重复的了。


<br>

## 💻 代码实现
```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));

        int count = 1;
        for(int i = 1; i < intervals.length; i++){
            if(intervals[i][0] < intervals[i-1][1]){
                intervals[i][1] = Math.min(intervals[i][1], intervals[i-1][1]);
            }
            else{
                count++;
            }
        }
        return intervals.length - count;
    }
}
```

<br>

## 763. 划分字母区间 
- 题目链接：[**LeetCode 763. Partition Labels**](https://leetcode.com/problems/partition-labels/)
- 关键词：**Greedy**

<br>

## 💡 思路
先找出每个字母出现的最迟的index，然后进行for loop，当当前index等于最迟index时，说明可以分割字母串，将这个字母串的长度放到list里面。

<br>

## 💻 代码实现
```java
class Solution {
    public List<Integer> partitionLabels(String s) {
        List<Integer> list = new LinkedList<>();
        int[] edge = new int[26];
        char[] chars = s.toCharArray();
        for(int i = 0; i < chars.length; i++){
            edge[chars[i] - 'a'] = i;
        }
        int idx = 0;
        int last = -1;
        for(int i = 0; i < chars.length; i++){
            idx = Math.max(idx, edge[chars[i] - 'a']);
            if(i == idx){
                list.add(i - last);
                last = i;
            }
        }
        return list;
    }
}
```

<br>

## 📝 今日心得
今天的内容都是处理重叠区域的，重点在于区域的划分，按照什么顺序来找。