# 📝 LeetCode 学习日志 Day 6

<br>

## 454. 四数相加II
- 题目链接：[**LeetCode 454. 4 Sum II**](https://leetcode.com/problems/4sum-ii/)
- 关键词：**HashMap**  

<br>

## 💡 思路
这道题就是比较经典需要用到HashMap的题目，先将前两个数相加，然后把相加的结果和出现次数放到HashMap里面，再把后两个数相加的相反数算出来，看这个相反数在HashMap里出现几次，将次数加到最终答案里。

<br>

## 💻 代码实现
```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        int count = 0;
        Map<Integer, Integer> check = new HashMap<>();
        
        for(int i: nums1){
            for(int j: nums2){
                int sum = i + j;
                check.put(sum, check.getOrDefault(sum, 0) + 1);
            }
        }

        for(int m: nums3){
            for(int n: nums4){
                count += check.getOrDefault(0-m-n, 0);
            }
        }

        return count;
    }
}
```

```python
class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        ans = {}
        count = 0
        for i in nums1:
            for j in nums2:
                ans[i + j] = ans.get(i + j, 0) + 1

        for m in nums3:
            for n in nums4:
                count += ans.get(0-m-n, 0)
        
        return count
```

<br>

## 383. 赎金信
- 题目链接：[**LeetCode 383. Ransom Note**](https://leetcode.com/problems/ransom-note/)
- 关键词：**List**

<br>

## 💡 思路
本题和 242.有效的字母异位词 是一个思路, 建立一个int list，然后将ransomNote字母出现的次数放到list里面，再把magazine字母出现的次数减去，最后看list里面是否有大于0的数字，大于0说明不满足条件。

<br>

## 💻 代码实现
```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        if (ransomNote.length() > magazine.length()) {
            return false;
        }
        int[] check = new int[26];

        for(int i = 0; i < ransomNote.length(); i++){
            check[ransomNote.charAt(i) - 'a']++;
        }
        for(int j = 0; j < magazine.length(); j++){
            check[magazine.charAt(j) - 'a']--;
        }
        for(int i: check){
            if(i > 0){
                return false;
            }
        }
        return true;
    }
}
```

```python
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        count = {}

        for ch in magazine:
            count[ch] = count.get(ch, 0) + 1

        for ch in ransomNote:
            if ch not in count:
                return False

            count[ch] -= 1

            if count[ch] < 0:
                return False

        return True
```

<br>

##  15. 三数之和
- 题目链接：[**LeetCode 15. 3Sum**](https://leetcode.com/problems/3sum/)
- 关键词：**Two Pointers**

<br>

## 💡 思路  
这道题用Two Pointers会比较快捷。先将整个list sort，然后从第一个数字开始循环，先判断第一个数字是不是大于0，如果大于0的话，因为已经排过序了，所以后续不可能有数字满足这个条件。再判断第一个数字是否跟之前做过循环的数字有重复，重复就跳过。确认完毕之后进入双指针环节，设定left为i+1， right为右边最后一个数字，然后看他们的sum跟0的关系来调整left and right。满足条件之后放入答案里，再对left和right进行去重，重复就跳过。

<br>

## 💻 代码实现
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(nums);

        for(int i = 0; i < nums.length; i++){
            if(nums[i] > 0){
                return ans;
            }
            if(i > 0 && nums[i-1] == nums[i]){
                continue;
            }

            int left = i + 1;
            int right = nums.length - 1;
            while(left < right){
                int sum = nums[i] + nums[left] + nums[right];
                if(sum > 0){
                    right--;
                }
                else if(sum < 0){
                    left++;
                }
                else{
                    ans.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    while(left < right && nums[left] == nums[left + 1]){
                        left++;
                    }
                    while(left < right && nums[right - 1] == nums[right]){
                        right--;
                    }

                    left++;
                    right--;
                }
            } 
        }
        return ans;
    }
}
```

```python
class Solution:
    def threeSum(self, nums: list[int]) -> list[list[int]]:
        ans = []
        nums.sort()

        for i in range(len(nums)):
            if nums[i] > 0:
                return ans
            if i > 0 and nums[i-1] == nums[i]:
                continue

            left = i + 1
            right = len(nums) - 1
            while left < right:
                sum = nums[i] + nums[left] + nums[right]
                if sum > 0:
                    right -= 1
                elif sum < 0:
                    left += 1
                else:
                    ans.append([nums[i], nums[left], nums[right]])
                    while(left < right and nums[left + 1] == nums[left]):
                        left += 1
                    while(left < right and nums[right - 1] == nums[right]):
                        right -= 1

                    left += 1
                    right -= 1
        return ans 
```

<br>

##  18. 四数之和
- 题目链接：[**LeetCode 18. 4Sum**]（https://leetcode.com/problems/4sum/）
- 关键词：**Two Pointers**

<br>

## 💡 思路  
这道题跟三数之和一样的，只不过就是多加一层循环。

<br>

## 💻 代码实现
```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(nums);

        for(int i = 0; i < nums.length; i++){
            if(nums[i] > target && nums[i] > 0){
                return ans;
            }
            if(i > 0 && nums[i-1] == nums[i]){
                continue;
            }
            for(int j = i + 1; j < nums.length; j++){
                if(nums[i] + nums[j] > target && nums[i] + nums[j] > 0){
                    break;
                }
                if(j > i+1 && nums[j-1] == nums[j]){
                    continue;
                }

                int left = j+1;
                int right = nums.length - 1;
                while(left < right){
                    int sum = nums[i] + nums[j] + nums[left] + nums[right];
                    if(sum > target){
                        right--;
                    }
                    else if(sum < target){
                        left++;
                    }
                    else{
                        ans.add(Arrays.asList(nums[i], nums[j], nums[left], nums[right]));
                        while(left < right && nums[left] == nums[left+1]) left++;
                        while(left < right && nums[right-1] == nums[right]) right--;
                        left++;
                        right--;
                    }
                }
            }
        }
        return ans;
    }
}
```

```python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        ans = []
        nums.sort()

        for i in range(len(nums)):
            if nums[i] > target and nums[i] > 0:
                return ans
            elif i > 0 and nums[i - 1] == nums[i]:
                continue
            for j in range(i + 1, len(nums)):
                if(nums[i] + nums[j] > target and nums[i] + nums[j] > 0):
                    break
                elif j > i + 1 and nums[j - 1] == nums[j]:
                    continue
                
                left = j + 1
                right = len(nums) - 1
                while left < right:
                    sum = nums[i] + nums[j] + nums[left] + nums[right]
                    if sum > target:
                        right -= 1
                    elif sum < target:
                        left += 1
                    else:
                        ans.append([nums[i], nums[j], nums[left], nums[right]])
                        while(left < right and nums[left + 1] == nums[left]):
                            left += 1
                        while(left < right and nums[right - 1] == nums[right]):
                            right -= 1
                        
                        left += 1
                        right -= 1

        return ans
```

<br>

## 📝 今日心得
三数之和和四数之和虽然看起来代码量比较吓人，但实际理解起来没有那么复杂，多多练习对于edge case的敏感度。HashMap和HashSet的一些特殊method，像getOrDefault这些，也需要多练多记。