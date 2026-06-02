# 📝 LeetCode 学习日志 Day 10

<br>

## 150. 逆波兰表达式求值
- 题目链接：[**LeetCode 150. Evaluate Reverse Polish Notation**](https://leetcode.com/problems/evaluate-reverse-polish-notation/)
- 关键词：**Stack**  

<br>

## 💡 思路
这道题相对而言比较简单，建立一个stack用ArrayDeque来实现，当这个token是数字时，加入到stack里面。当这个token是运算符号时，pop两个数字从stack里面，进行运算，然后把结果重新push到stack里面。最后stack剩下的那个数字就是结果了。

<br>

## 💻 代码实现
```java
class Solution {
    public int evalRPN(String[] tokens) {
        Deque<Integer> stack = new ArrayDeque<>();
        for (int i = 0; i < tokens.length; i++) {
            String token = tokens[i];
            if (token.equals("+")) {
                int first = stack.pop();
                int second = stack.pop();
                stack.push(second + first);
            } else if (token.equals("-")) {
                int first = stack.pop();
                int second = stack.pop();
                stack.push(second - first);
            } else if (token.equals("*")) {
                int first = stack.pop();
                int second = stack.pop();
                stack.push(second * first);
            } else if (token.equals("/")) {
                int first = stack.pop();
                int second = stack.pop();
                stack.push(second / first);
            } else {
                stack.push(Integer.valueOf(token));
            }
        }
        return stack.pop();
    }
}
```

<br>

## 239. 滑动窗口最大值
- 题目链接：[**LeetCode 239. Sliding Window Maximum**](https://leetcode.com/problems/sliding-window-maximum/)
- 关键词：**Deque, ArrayDeque**

<br>

## 💡 思路
这道题比较的有难度。需要用到单调队列的思想。建立一个deque单调队列，从大到小来放index，当deque里第一个index不在sliding window的范围时poll出来。当deque的末尾数字小于将要加进去的数字时，将末尾数字poll出来，因为他永远不可能成为sliding window里最大的数字。将这个index加入到deque里面。当循环进入sliding window时，每一次移动窗口都把最大的数字，也就是deque的最前端，加入到答案里面去。

<br>

## 💻 代码实现
```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int length = nums.length;
        int[] ans = new int[length - k + 1];
        int count = 0;
        Deque<Integer> deque = new ArrayDeque<>();

        for(int i = 0; i < nums.length; i++){
            while(!deque.isEmpty() && deque.peek() < i - k + 1){
                deque.poll();
            }

            while(!deque.isEmpty() && nums[deque.peekLast()] < nums[i]){
                deque.pollLast();
            }

            deque.offer(i);

            if(i >= k - 1){
                ans[count] = nums[deque.peek()];
                count++;
            }
        }

        return ans;
    }
}
```

<br>

## 347.前 K 个高频元素
- 题目链接：[**LeetCode 347. Top K Frequent Elements**](https://leetcode.com/problems/top-k-frequent-elements/)
- 关键词：**PriorityQueue**

<br>

## 💡 思路
这道题比较的有难度，第一次做可能做不出来。这道题需要同时考虑出现频率最高的元素和出现的频率，所以这里采用的是Min-Heap的方式，通过PriorityQueue来实现。

先用一个Map来统计所有的元素以及他的出现频率，然后用PriorityQueue的方式，将元素和频率看作一个int数组，进行排序，当pq的size小于k，加入map里的元素，当size超过k时，如果新的元素频率大于pq里最小的频率，则update。最后将pq里的数字导出到一个int数组里。

<br>

## 💻 代码实现
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int num: nums){
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        PriorityQueue<int[]> pq = new PriorityQueue<>((o1, o2) -> o1[1] - o2[1]);
        for(Map.Entry<Integer, Integer> entry: map.entrySet()){
            if(pq.size() < k){
                pq.add(new int[]{entry.getKey(), entry.getValue()});
            }
            else{
                if(entry.getValue() > pq.peek()[1]){
                    pq.poll();
                    pq.add(new int[]{entry.getKey(), entry.getValue()});
                }
            }
        }

        int[] res = new int[k];

        for(int i = k-1; i >= 0; i--){
            res[i] = pq.poll()[0];
        }

        return res;
    }
}
```

<br>

## 📝 今日心得
今天的题目还是相对比较有难度的，第一次做的时候不容易想出来。今天做题时发现还是对stack和queue的一些功能不是很熟悉，比如push是stack用来加元素的，而queue会用add/offer，deque和queue一样，然后priorityqueue是用add。今天还涉及到了priorityqueue来实现Min-Heap，也算是复习和重新捡起印象，多练就会熟练了。