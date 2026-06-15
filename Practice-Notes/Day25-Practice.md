# 📝 LeetCode 学习日志 Day 25

<br>

## 134. 加油站
- 题目链接：[**LeetCode 134. Gas Station**](https://leetcode.com/problems/gas-station/)
- 关键词：**Greedy**  

<br>

## 💡 思路
这道题采用了贪心算法,是一个非常巧妙的思路。首先很明显的就是，如果totalGas < totalCost的话，是肯定跑不完一圈的。

那重点就在于怎么去寻找可以跑完一圈的那个点。可以通过计算一段区间的totalSum，如果这个区间的totalSum < 0, 说明不是从里面的这个点开始的，那么start点就应该是 i + 1。


<br>

## 💻 代码实现
```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int curSum = 0;
        int totalSum = 0;
        int index = 0;
        for(int i = 0; i < gas.length; i++){
            curSum += gas[i] - cost[i];
            totalSum += gas[i] - cost[i];
            if(curSum < 0){
                index = i + 1;
                curSum = 0;
            }
        }
        if(totalSum < 0) return -1;
        return index;
    }
}
```

<br>

## 135. 分发糖果
- 题目链接：[**LeetCode 135. Candy**](https://leetcode.com/problems/candy/)
- 关键词：**Greedy**

<br>

## 💡 思路
这道题采用的是贪心算法，思路非常的巧妙。先跟左邻居进行比较，再跟右邻居进行比较。用一个int array来记录每个孩子的糖果数量。

先进行一遍从左到右的遍历，起始值的candy设为1。当右边rating比左边大时，右边的candy数量就是左边的 + 1。

再进行一遍从右到左的遍历，当左边rating比右边大时，比较array里面的的candy数量和右边 + 1的数量哪个大，就取哪个，确保左边的candy数量一定大于两边的。


<br>

## 💻 代码实现
```java
class Solution {
    public int candy(int[] ratings) {
        int len = ratings.length;
        int[] candy = new int[len];
        candy[0] = 1;
        for(int i = 1; i < ratings.length; i++){
            candy[i] = ratings[i] > ratings[i - 1] ? candy[i - 1] + 1 : 1;
        }

        for(int i = len - 2; i >= 0; i--){
            if(ratings[i] > ratings[i + 1])
            candy[i] = Math.max(candy[i + 1] + 1, candy[i]);
        }

        int sum = 0;
        for(int num: candy){
            sum += num;
        }
        return sum;
    }
}
```

<br>

## 860. 柠檬水找零
- 题目链接：[**LeetCode 860. Lemonade Change**](https://leetcode.com/problems/lemonade-change/)
- 关键词：**Greedy**

<br>

## 💡 思路
这道题其实非常简单，只需要控制好5元和10元的张数就行，有以下三种情况：

 - 情况一：账单是5，直接收下。
 - 情况二：账单是10，消耗一个5，增加一个10
 - 情况三：账单是20，优先消耗一个10和一个5，如果不够，再消耗三个5

为什么情况三要优先消耗10呢，因为10只能给20找零钱，而5更万能。

<br>

## 💻 代码实现
```java
class Solution {
    public boolean lemonadeChange(int[] bills) {
        int five = 0;
        int ten = 0;
        for(int i = 0; i < bills.length; i++){
            if(bills[i] == 5){
                five++;
            }
            else if(bills[i] == 10){
                five--;
                ten++;
            }
            else if(bills[i] == 20){
                if(ten > 0){
                    ten--;
                    five--;
                }
                else{
                    five -= 3;
                }
            }
            if(five < 0 || ten < 0) return false;
        }
        return true;
    }
}
```

<br>

## 406. 根据身高重建队列
- 题目链接：[**LeetCode 406. Queue Reconstruction by Height**](https://leetcode.com/problems/queue-reconstruction-by-height/)
- 关键词：**Greedy**

<br>

## 💡 思路
这道题跟135有些类似，其技巧都是确定一边然后贪心另一边，两边一起考虑，就会顾此失彼。

先以高度来排序，从高到低，相同高度情况下k小的排在前面。

之后再以k的值来决定插入linkedlist的index，保证有k个人高于当前这个人。



<br>

## 💻 代码实现
```java
class Solution {
    public int[][] reconstructQueue(int[][] people) {
        Arrays.sort(people, (a, b) -> {
            if(a[0] == b[0]) return a[1] - b [1];
            return b[0] - a[0];
        });

        LinkedList<int[]> que = new LinkedList<>();

        for(int[] p: people){
            que.add(p[1], p);
        }

        return que.toArray(new int[people.length][]);
    }
}
```

<br>

## 📝 今日心得
今天是对于贪心算法的一个介绍，有的题目的贪心算法就比较简单，有的就比较复杂。对于需要考虑两方面排序的问题，其技巧都是确定一边然后贪心另一边，两边一起考虑，就会顾此失彼。