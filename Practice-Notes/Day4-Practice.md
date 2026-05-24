# 📝 LeetCode 学习日志 Day 4

<br>

## 24. 两两交换链表中的节点
- 题目链接：[**LeetCode 24. Swap Nodes in Pairs**](https://leetcode.com/problems/swap-nodes-in-pairs/)
- 关键词：**Linked List, Two Pointers**  

<br>

## 💡 思路
这道题的思路跟LeetCode 206 Reverse Linked List是一样的。**先加入一个dummy node 方便操作**，然后将dummy node，firstNode，secondNode，三个看作一个整体进行操作。剩余步骤同206。

<br>

## 💻 代码实现
```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode temp, firstNode, secondNode;
        ListNode curNode = dummy;
        while(curNode.next != null && curNode.next.next != null){
            temp = curNode.next.next.next;
            firstNode = curNode.next;
            secondNode = curNode.next.next;
            curNode.next = secondNode;
            secondNode.next = firstNode;
            firstNode.next = temp;
            curNode = firstNode;
        }

        return dummy.next;
    }
}
```

```python
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(0)
        dummy.next = head
        prev = dummy
        cur = head
        while cur and cur.next:
            temp = cur.next
            prev.next = temp
            cur.next = temp.next
            temp.next = cur
            prev = cur
            cur = cur.next
        return dummy.next
```

<br>

##  19. 删除链表的倒数第N个节点
- 题目链接：[**LeetCode 19. Remove Nth Node From End of List**](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
- 关键词：**Linked List, Two Pointers**

<br>

## 💡 思路
这道题第一次运用了快慢指针的思路，这个思路在linked list里面比较常见。首先加入**dummy node**， 将快慢指针同时指向dummy node，然后将快指针先移动n次，再同时移动快慢指针，当快指针到队尾时停下，此时慢指针正好指向要删除node前的一个node。

<br>

## 💻 代码实现
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode slow = dummy;
        ListNode fast = dummy;
        for(int i = 0; i < n; i++){
            fast = fast.next;
        }

        while(fast.next != null){
            slow = slow.next;
            fast = fast.next;
        }

        slow.next = slow.next.next;
        return dummy.next;
    }
}
```

```python
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0)
        dummy.next = head
        fast = dummy
        slow = dummy
        for i in range(n):
            fast = fast.next
        
        while fast.next and slow.next:
            fast = fast.next
            slow = slow.next
        slow.next = slow.next.next
        return dummy.next
```

<br>

##  160. 链表相交
- 题目链接：[**LeetCode 160. Intersection of Two Linked Lists**](https://leetcode.com/problems/intersection-of-two-linked-lists/)
- 关键词：**Linked List, Two Pointers**

<br>

## 💡 思路  
这道题的思路非常巧妙，第一次做的话基本上想不到，将两个指针分别设置于两个链表的head，然后同时移动，当一个指针走到链表的结尾时，让他重新回到另一个链表的head，这样将两个链表链接起来，两个指针第二次经过相交点的路程就是一样的了。

<br>

## 💻 代码实现
```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode p1 = headA;
        ListNode p2 = headB;

        while(p1 != p2){
            p1 = p1 == null ? headB : p1.next;
            p2 = p2 == null ? headA : p2.next;
        }

        return p1;
    }
}
```

```python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        nodeA = headA
        nodeB = headB
        
        while nodeA != nodeB:
            nodeA = nodeA.next if nodeA else headB
            nodeB = nodeB.next if nodeB else headA
        return nodeA
```

<br>

##  142. 环形链表II
- 题目链接：[**LeetCode 142. Linked List II**]（https://leetcode.com/problems/linked-list-cycle-ii/）
- 关键词：**Linked List, Two Pointers**

<br>

## 💡 思路  
这道题的思路非常巧妙，第一次做的话基本上想不到，也非常的反直觉。先将快慢指针同时指向head，然后快指针每次移动两个node，慢指针每次移动一个node。如果快指针到结尾都没跟慢指针相遇，说明没有loop。如果快慢指针相遇了，说明有loop，此时再设定一个指针在head，然后这个指针跟慢指针每次移动一个node，最终他们会相遇在loop的开始点。

<br>

## 💻 代码实现
```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;

        while(fast != null && fast.next != null){
            fast = fast.next.next;
            slow = slow.next;

            if(fast == slow){
                ListNode target = head;
                while(target != slow){
                    target = target.next;
                    slow = slow.next;
                }
                return target;
            }
        }
        return null;
    }
}
```

```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        fast = head
        slow = head

        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next

            if fast is slow:
                temp = head
                while temp is not slow:
                    temp = temp.next
                    slow = slow.next
                return temp
        return None
```

<br>

## 📝 今日心得
今天的这四道题目相对而言是比较有难度的，如果是第一次做的话很难想到办法。其中160和142这两道比较的反直觉，需要做完多加深巩固印象，不是能靠暴力解决能实现的。在linked list里面比较重要的两点就是添加dummy node和使用快慢指针，会很方便。
