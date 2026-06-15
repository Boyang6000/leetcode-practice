# 📝 LeetCode 学习日志 Day 27

<br>

## 56. 合并区间
- 题目链接：[**LeetCode 56. Merge Intervals**](https://leetcode.com/problems/merge-intervals/)
- 关键词：**Greedy**  

<br>

## 💡 思路
这道题其实跟452和435是一样的。先确定两个interval是否重合，如果重合，就调整interval的末尾来cover两个interval。如果不重合就直接把这个interval加入到result里面。

<br>

## 💻 代码实现
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        List<int[]> result = new LinkedList<>();
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        result.add(intervals[0]);
        for(int i = 1; i < intervals.length; i++){
            if(intervals[i][0] <= result.getLast()[1]){
                int start = result.getLast()[0];
                int end = Math.max(intervals[i][1], result.getLast()[1]);
                result.removeLast();
                result.add(new int[]{start, end});
            }
            else{
                result.add(intervals[i]);
            }
        }
        return result.toArray(new int[result.size()][]);
    }
}
```

<br>

## 738. 单调递增的数字
- 题目链接：[**LeetCode 738. Monotone Increasing Digits**](https://leetcode.com/problems/monotone-increasing-digits/)
- 关键词：**Greedy**

<br>

## 💡 思路
这道题比较的巧妙，需要通过倒序的方式来处理，当当前index的数字比后面的数字大时，当前index数字减1，后面的数字变成9。

为了方便操作，可以先把数字变成string模式，最后再把string变成int。


<br>

## 💻 代码实现
```java
class Solution {
    public int monotoneIncreasingDigits(int n) {
        String s = String.valueOf(n);
        char[] chars = s.toCharArray();
        int start = s.length();
        for(int i = s.length() - 2; i >= 0; i--){
            if(chars[i] > chars[i + 1]){
                chars[i]--;
                start = i + 1;
            }
        }
        for(int i = start; i < s.length(); i++){
            chars[i] = '9';
        }
        return Integer.parseInt(String.valueOf(chars));
    }
}
```

<br>

## 📝 今日心得
今天的内容都是处理重叠区域的，重点在于区域的划分，按照什么顺序来找。贪心算法还是很不好想的，当看到答案时又会发现其实思路是很简单的。