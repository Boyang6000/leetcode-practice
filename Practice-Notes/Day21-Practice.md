# 📝 LeetCode 学习日志 Day 21

<br>

## 93. 复原IP地址 
- 题目链接：[**LeetCode 93. Restore IP Address**](https://leetcode.com/problems/restore-ip-addresses/)
- 关键词：**Backtracking**  

<br>

## 💡 思路
这道题也是使用了回溯算法。重点在于怎么把s分成四段然后验证每一段是否是valid ip。这里我们增加了一个变量pointNum来记录加了几个.

判断段位是否是有效段位主要考虑到如下三点：

 - 段位以0为开头的数字不合法
 - 段位里有非正整数字符不合法
 - 段位如果大于255了不合法


<br>

## 💻 代码实现
```java
class Solution {
    List<String> result = new ArrayList<>();
    public List<String> restoreIpAddresses(String s) {
        if(s.length() > 12) return result;
        backtracking(s, 0, 0);
        return result;
    }

    private void backtracking(String s, int startIndex, int pointNum){
        if(pointNum == 3){
            if(isValid(s, startIndex, s.length() - 1)){
                result.add(s);
            }
            return;
        }

        for(int i = startIndex; i < s.length(); i++){
            if(isValid(s, startIndex, i)){
                s = s.substring(0, i + 1) + "." + s.substring(i + 1);
                pointNum++;
                backtracking(s, i + 2, pointNum);
                pointNum--;
                s = s.substring(0, i + 1) + s.substring(i + 2);
            }
            else{
                break;
            }
        }
    }

    private boolean isValid(String s, int start, int end){
        if(start > end) return false;
        if(s.charAt(start) == '0' && start != end) return false;
        int num = 0;
        for(int i = start; i <= end; i++){
            if(s.charAt(i) >'9' || s.charAt(i) < '0') return false;
            num = num * 10 + (s.charAt(i) - '0');
            if(num > 255) return false;
        }
        return true;
    }
}
```

<br>

## 78. 子集
- 题目链接：[**LeetCode 78. Subsets**](https://leetcode.com/problems/subsets/)
- 关键词：**Backtracking**

<br>

## 💡 思路
这道题就是比较基础的backtracking运用。


<br>

## 💻 代码实现
```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    LinkedList<Integer> item = new LinkedList<>();
    public List<List<Integer>> subsets(int[] nums) {
        if(nums == null || nums.length == 0) return result;
        backtracking(nums, 0);
        return result;
    }

    private void backtracking(int[] nums, int startIndex){
        result.add(new ArrayList<>(item));
        if(startIndex >= nums.length) return;
        for(int i = startIndex; i < nums.length; i++){
            item.add(nums[i]);
            backtracking(nums, i + 1);
            item.removeLast();
        }
    }
}
```

<br>

## 90. 子集II
- 题目链接：[**LeetCode 90. Subsets II**](https://leetcode.com/problems/subsets-ii/)
- 关键词：**Backtracking**

<br>

## 💡 思路
这道题的思路跟78是一样的，只不过多了一个去重，去重之前需要先把array sort一下，这样当当前index的数字和前一个index数字相同时，直接continue。

<br>

## 💻 代码实现
```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    LinkedList<Integer> path = new LinkedList<>();
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        backtracking(nums, 0);
        return result;
    }

    private void backtracking(int[] nums, int startIndex){
        result.add(new ArrayList<>(path));
        for(int i = startIndex; i < nums.length; i++){
            if(i > startIndex && nums[i] == nums[i - 1]) continue;
            path.add(nums[i]);
            backtracking(nums, i + 1);
            path.removeLast();
        }
    }
}
```

<br>

## 📝 今日心得
今天的题目是对回溯的一个练习，回溯和递归是类似的逻辑，理解起来会有些难度，需要熟练掌握回溯的写法，对于不同情况的运用随机应变。