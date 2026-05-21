# 📝 LeetCode 学习日志 Day 1

<br>

## 704. 二分查找
- 题目链接：[**LeetCode 704. Binary Search**](https://leetcode.com/problems/binary-search/)
- 关键词：**Binary Search**  

<br>

## 💡 思路
运用二分查找(Binary Search)，在 **左闭右闭区间** `[left, right]` 内查找 target：  

<br>

## 💻 代码实现
```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2; // 避免溢出
            if (nums[mid] > target) {
                right = mid - 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                return mid;
            }
        }
        return -1;
    }
}
```

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] > target:
                right = mid - 1
            else:
                left = mid + 1
        return -1
```

<br>

##  27. 移除元素
- 题目链接：[**LeetCode 27. Remove Element**](https://leetcode.com/problems/remove-element/)
- 关键词：**Two Pointers**

<br>

## 💡 思路
运用Two Pointers，一个指针记录当前的index，另一个指针记录不需要remove的数量，如果当前index不需要remove，就放在另一个指针的位置然后update  

<br>

## 💻 代码实现
```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int count = 0;
        for(int i = 0; i < nums.length; i++){
            if(nums[i] != val){
                nums[count] = nums[i];
                count++;
            }
        }

        return count;
    }
}
```

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        index = 0
        for i in range(len(nums)):
            if nums[i] != val:
                nums[index] = nums[i]
                index += 1
        return index
```

<br>

##  977. 有序数组的平方
- 题目链接：[**LeetCode 977. Squares of a Sorted Array**](https://leetcode.com/problems/squares-of-a-sorted-array/)
- 关键词：**Two Pointers**

<br>

## 💡 思路  
先将所有的数字根据他们的绝对值大小进行排序，用两个指针分别指向left和right进行大小比较，将另一个指针放在新的Array的队尾，将大的数字放在另一个指针的位置，然后update所有指针的位置。当排序完成时，将每个数字平方即可

<br>

## 💻 代码实现
```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int index = nums.length - 1;
        int left = 0;
        int right = nums.length - 1;
        int[] ans = new int[nums.length];

        while(left <= right){
            if(Math.abs(nums[left]) > Math.abs(nums[right])){
                ans[index] = nums[left];
                index--;
                left++;
            }
            else{
                ans[index] = nums[right];
                index--;
                right--;
            }
        }

        for(int i = 0; i < ans.length; i++){
            ans[i] = ans[i] * ans[i];
        }

        return ans;
    }
}
```

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        nums = [abs(x) for x in nums]
        nums.sort()
        nums = [x**2 for x in nums]
        return nums
```

<br>

## 📝 今日心得
作为Day 1的题目，这三道题目都是比较基础的，其中Binary Search和Two Pointers这两个思想都是运用比较广泛的，这几道题目也是自己练过很多遍的，基本不会出现问题。希望能将这两个思路继续运用到别的不同的题目上面去
