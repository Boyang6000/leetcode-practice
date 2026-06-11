# 📝 LeetCode 学习日志 Day 22

<br>

## 491. 递增子序列 
- 题目链接：[**LeetCode 491. Non-decreasing Subsequences**](https://leetcode.com/problems/non-decreasing-subsequences/)
- 关键词：**Backtracking**  

<br>

## 💡 思路
这道题也是运用了回溯法来实现的。这里需要注意两点，第一点是检查path size是不是大于1，如果是的话就把这个path放到result里面。其次是判断nums[i]是否加入到path里面。如果nums[i]小于path最后一位，则不加入；如果nums[i]已经用过了（用used数组来判断是否用过），则不考虑加入。


<br>

## 💻 代码实现
```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    LinkedList<Integer> path = new LinkedList<>();
    public List<List<Integer>> findSubsequences(int[] nums) {
        backtracking(nums, 0);
        return result;
    }

    private void backtracking(int[] nums, int startIndex){
        if(path.size() > 1){
            result.add(new ArrayList<>(path));
        }
        int[] used = new int[201];
        for(int i = startIndex; i < nums.length; i++){
            if(!path.isEmpty() && nums[i] < path.get(path.size() - 1) || (used[nums[i] + 100] == 1)){
                continue;
            }
            used[nums[i] + 100] = 1;
            path.add(nums[i]);
            backtracking(nums, i + 1);
            path.remove(path.size() - 1);
        }
    }
}
```

<br>

## 46. 全排列
- 题目链接：[**LeetCode 46. Permutations**](https://leetcode.com/problems/permutations/)
- 关键词：**Backtracking**

<br>

## 💡 思路
这道题就是比较基础的backtracking运用, 对于重复的数字，这里可以运用到linkedlist里面的method contains来检查是否已经选取过元素。


<br>

## 💻 代码实现
```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    LinkedList<Integer> path = new LinkedList<>();
    public List<List<Integer>> permute(int[] nums) {
        backtracking(nums, 0);
        return result;
    }

    private void backtracking(int[] nums, int startIndex){
        if(path.size() == nums.length){
            result.add(new ArrayList<>(path));
        }
        for(int i = startIndex; i < nums.length; i++){
            if(path.contains(nums[i])){
                continue;
            }
            path.add(nums[i]);
            backtracking(nums, startIndex);
            path.removeLast();
        }
    }
}
```

<br>

## 47. 全排列 II
- 题目链接：[**LeetCode 47. Permutations II**](https://leetcode.com/problems/permutations-ii/)
- 关键词：**Backtracking**

<br>

## 💡 思路
这道题主要是考虑去重的逻辑，当这个index的数字与前一个index相等并且前一个index已经被读取了,那就跳过。

<br>

## 💻 代码实现
```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    LinkedList<Integer> path = new LinkedList<>();
    public List<List<Integer>> permuteUnique(int[] nums) {
        boolean[] used = new boolean[nums.length];
        Arrays.fill(used, false);
        Arrays.sort(nums);
        backtracking(nums, used);
        return result;
    }

    private void backtracking(int[] nums, boolean[] used){
        if(path.size() == nums.length){
            result.add(new ArrayList<>(path));
            return;
        }
        for(int i = 0; i < nums.length; i++){
            if(i > 0 && nums[i] == nums[i - 1] && used[i - 1] == false){
                continue;
            }
            if(used[i] == false){
                used[i] = true;
                path.add(nums[i]);
                backtracking(nums, used);
                path.removeLast();
                used[i] = false;
            }
        }
    }
}
```

<br>

## 📝 今日心得
今天的题目是对回溯的一个练习，重点运用到了used array去进行去重，去重之前一定要先进行sort。