# 📝 LeetCode 学习日志 Day 5

<br>

## 242. 有效的字母异位词
- 题目链接：[**LeetCode 242. Valid Anagram**](https://leetcode.com/problems/valid-anagram/)
- 关键词：**HashTable**  

<br>

## 💡 思路
这道题因为长度的限制，所以可以使用list来代替hashmap。先创建一个int list来存放每个字母出现的次数，然后循环s来看每个字母出现多少次，出现一次就在int list相对应的位置加1。然后再看t每个字母出现多少次，出现一次就在int list相对应的位置减1。最后来看是否int list里面每个数字都是0，如果不是就return false。

<br>

## 💻 代码实现
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        int[] ans = new int[26];

        for(int i = 0; i < s.length(); i++){
            ans[s.charAt(i) - 'a']++;
        }

        for(int j = 0; j < t.length(); j++){
            ans[t.charAt(j) - 'a']--;
        }

        for(int k: ans){
            if(k != 0){
                return false;
            }
        }
        return true;
    }
}
```

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        dictS = {}
        for i in range(len(s)):
            dictS[s[i]] = dictS.get(s[i], 0) + 1
        for j in range(len(t)):
            if t[j] in dictS:
                dictS[t[j]] = dictS[t[j]] - 1
                if dictS[t[j]] < 0:
                    return False
            else:
                return False
        return True
```

<br>

##  349. 两个数组的交集
- 题目链接：[**LeetCode 349. Intersection of Two Arrays**](https://leetcode.com/problems/intersection-of-two-arrays/)
- 关键词：**HashSet**

<br>

## 💡 思路
因为HashSet不允许出现重复的值，重复的值添加进去将会被忽略，所以这里我们使用HashSet。先创建第一个HashSet，将nums1里面的数字都添加进去，然后再创建第二个HashSet，如果num2的数字出现在第一个HashSet里，将这个数字加入到第二个HashSet里面。这样既确保了这个数字同时出现在两个list里面，并且答案数字不会重复。最后将答案HashSet里面的数字转化成list。

<br>

## 💻 代码实现
```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> check = new HashSet<>();
        Set<Integer> ans = new HashSet<>();

        for(int i: nums1){
            check.add(i);
        }

        for(int j: nums2){
            if(check.contains(j)){
                ans.add(j);
            }
        }

        int[] result = new int[ans.size()];
        int count = 0;
        for(int i: ans){
            result[count] = i;
            count++;
        }

        return result;
    }
}
```

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        return list(set(nums1) & set(nums2))
```

<br>

##  202. 快乐数
- 题目链接：[**LeetCode 202. Happy Number**](https://leetcode.com/problems/happy-number/)
- 关键词：**HashSet**

<br>

## 💡 思路  
这道题先要去理解什么情况下是happy number什么情况下不是。当运算结果等于1的时候就是happy number，如果运算过程中出现了重复结果就不是。储存每次结果跟重复挂钩时优先考虑HashSet。

这道题分为两步：
- 先写一个method来运算happy。先算这个数字mod10剩下的余数，就是最右边的这个digit。然后平方再加入到sum里面去，最后将这个数字除以10，就进入到下一个digit的运算。重复循环直至所有digit的平方都加入到了sum里面。
- 主要的method来看这个数字是否是happy number。先创建一个HashSet来储存所有出现的结果。当这个数字不等于1或者没有出现在HashSet里面时，将他加入到HashSet里，然后再进行happy运算，重复这个过程。


<br>

## 💻 代码实现
```java
class Solution {
    public boolean isHappy(int n) {
        Set<Integer> check = new HashSet<>();
        while(n != 1 && !(check.contains(n))){
            check.add(n);
            n = happy(n);
        }

        return n == 1;
    }

    public int happy(int n){
        int sum = 0;
        while(n > 0){
            int digit = n % 10;
            sum += digit * digit;
            n = n / 10;
        }
        return sum;
    }
}
```

```python
class Solution:
    def isHappy(self, n: int) -> bool:
        seen = set()
        while n != 1:
            n = sum(int(i)**2 for i in str(n))
            if n in seen:
                return False
            seen.add(n)
        return True
```

<br>

##  1. 两数之和
- 题目链接：[**LeetCode 1. Two Sum**]（https://leetcode.com/problems/two-sum/）
- 关键词：**HashMap**

<br>

## 💡 思路  
这道题是好几道经典题目的开始，比如三数之和和四数之和。创建一个HashMap来储存数字和他的index。计算target和当前index数字的差，如果他们的差在这个HashMap里，就return这两个数字的index。如果不在这个HashMap里面，就将当前的数字和他的index加入到HashMap里面。

<br>

## 💻 代码实现
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> check = new HashMap<>();
        
        for(int i = 0; i < nums.length; i++){
            int diff = target - nums[i];
            if(check.containsKey(diff)){
                return new int[]{check.get(diff), i};
            }
            else{
                check.put(nums[i], i);
            }
        }

        return null;
    }
}
```

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        check = {}

        for i in range(len(nums)):
            if nums[i] in check:
                return [check[nums[i]], i]
            diff = target - nums[i]
            check[diff] = i
```

<br>

## 📝 今日心得
HashMap和HashSet一直以来就是我比较薄弱的地方，一方面是平时运用的少，另一方面是自己内心里还是有点恐惧这个题型，需要更多的练习巩固加强对HashMap和HashSet的运用。今天主要是帮助分别在什么情况下运用HashMap和HashSet，当需要考虑过滤重复值的时候运用HashSet，然后当需要考虑存储两个值，例如数字和他的index时，就需要运用HashMap。