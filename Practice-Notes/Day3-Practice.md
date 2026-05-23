# 📝 LeetCode 学习日志 Day 3

<br>

## 203. 移除链表元素
- 题目链接：[**LeetCode 203. Remove Linked List Elements**](https://leetcode.com/problems/remove-linked-list-elements/)
- 关键词：**Linked List**  

<br>

## 💡 思路
这是一道非常基础的Linked List功能的实现。所有的Linked List题目首先想到的就是加一个dummy node，这会使整个过程变得更加简单和丝滑。加一个dummy node在head前面，然后设定dummy node为curNode，判断curNode.next是否需要删除，需要删除就将curNode.next连接到下一个，然后判断现在的curNode.next是否需要删除。不需要删除的话直接移动curNode到下一个。  

<br>

## 💻 代码实现
```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode curNode = dummy;
        while(curNode.next != null){
            if(curNode.next.val == val){
                curNode.next = curNode.next.next;
            }
            else{
                curNode = curNode.next;
            }
        }

        return dummy.next;
    }
}
```

```python
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        dummy = ListNode(0)
        dummy.next = head
        cur = dummy
        while cur.next:
            if cur.next.val == val:
                cur.next = cur.next.next
            else:
                cur = cur.next
        return dummy.next
```

<br>

##  707.设计链表
- 题目链接：[**LeetCode 707. Design Linked List**](https://leetcode.com/problems/design-linked-list/)
- 关键词：**Linked List**

<br>

## 💡 思路
这是一道非常全面考察Linked List基本method的implementation

**考虑将已经做好的method运用到其他的method里面去，减少代码量**

- **Initialization**：
    - 创建一个Node Class，里面包含Node的value和下一个Node，然后Initialize Node
    - 创建Linked List，里面包含size，来统计一共有多少node，还有head node。**做题时尽量考虑dummy node为head node**，这样写method implementation更加方便。

- **Get**：
    - 考虑index是否valid，如果not valid就return -1
    - 设定最开始node为curNode，iterate到指定的index然后return value

- **AddAtHead**:
    - 将dummy node的下一个node存储在temp里
    - 把新的node加到dummy node之后
    - 将temp node加到新的node后面
    - Update Size

- **AddAtTail**：
    - 循环至最后一个node，将新的node加到最后一个node之后
    - Update Size

- **AddAtIndex**：
    - Index小于等于0时，将node加到head，**运用AddAtHead**
    - Index等于size时，将node加到tail，**运用AddAtTail**
    - Index is not valid，return void
    - 找到加入index之前一位的node
    - 将这个node.next加入到新的node之后
    - 再将新的node加入到这个node后面
    - Update Size

- **DeleteAtIndex**：
    - 如果index is not valid，return null
    - 找到删除index之前一位的node
    - 将这个node.next链接到node.next.next
    - Update Size

<br>

## 💻 代码实现
```java
class MyLinkedList {
    class Node {
        int val;
        Node next;
        Node(int val) { this.val = val; }
    }

    private int size;
    private final Node head; // sentinel

    public MyLinkedList() {
        this.size = 0;
        this.head = new Node(0);
    }

    public int get(int index) {
        if (index < 0 || index >= size) return -1;
        Node cur = head.next;          // first real node
        for (int i = 0; i < index; i++) cur = cur.next;
        return cur.val;
    }

    public void addAtHead(int val) {
        Node node = new Node(val);
        node.next = head.next;
        head.next = node;
        size++;
    }

    public void addAtTail(int val) {
        Node cur = head;
        while (cur.next != null) cur = cur.next;
        cur.next = new Node(val);
        size++;
    }

    public void addAtIndex(int index, int val) {
        if (index <= 0) {              // treat negative as 0
            addAtHead(val);
            return;
        }
        if (index == size) {           // append
            addAtTail(val);
            return;
        }
        if (index > size) return;      // out of bounds

        // insert before the current index-th node: find predecessor
        Node pred = head;
        for (int i = 0; i < index; i++) pred = pred.next;
        Node node = new Node(val);
        node.next = pred.next;
        pred.next = node;
        size++;
    }

    public void deleteAtIndex(int index) {
        if (index < 0 || index >= size) return;
        Node pred = head;
        for (int i = 0; i < index; i++) pred = pred.next;
        pred.next = pred.next.next;
        size--;
    }
}
```

```python
class ListNode:
    def __init__(self, val=0, next = None):
        self.val = val
        self.next = next
class MyLinkedList:

    def __init__(self):
        self.dummy = ListNode(0)
        self.size = 0

    def get(self, index: int) -> int:
        if index < 0 or index >= self.size:
            return -1
        cur = self.dummy.next
        for i in range(index):
            cur = cur.next
        return cur.val


    def addAtHead(self, val: int) -> None:
        new = ListNode(val)
        new.next = self.dummy.next
        self.dummy.next = new
        self.size += 1

    def addAtTail(self, val: int) -> None:
        cur = self.dummy
        while cur.next:
            cur = cur.next
        new = ListNode(val)
        cur.next = new
        self.size += 1

    def addAtIndex(self, index: int, val: int) -> None:
        if index > self.size:
            return
        
        cur = self.dummy
        for i in range(index):
            cur = cur.next
        new = ListNode(val)
        new.next = cur.next
        cur.next = new
        self.size += 1

    def deleteAtIndex(self, index: int) -> None:
        if index >= self.size:
            return
        cur = self.dummy
        for i in range(index):
            cur = cur.next
        cur.next = cur.next.next
        self.size -= 1
```

<br>

##  206. 反转链表
- 题目链接：[**LeetCode 206. Reverse Linked List**](https://leetcode.com/problems/reverse-linked-list/)
- 关键词：**Two Pointers, Linked List**

<br>

## 💡 思路  
这道题的思路非常巧妙，以1 -> 2 -> 3 -> 4 -> 5为例，在前面增加一个dummy node，变成 0 -> 1 -> 2 -> 3 -> 4 -> 5, 然后一个指针指向0，另一个指针指向1，进行翻转。

<br>

## 💻 代码实现
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode cur = head;
        ListNode temp = null;
        while(cur != null){
            temp = cur.next;
            cur.next = prev;
            prev = cur;
            cur = temp;
        }

        return prev;
    }
}
```

<br>

## 📝 今日心得
今天的题目都是关于Linked List，涉及到比较基础的一些method的implementation，在做关于linked list的题目时一定要注意while loop结束的点，以及你的curNode移动到了哪里。关于最基本的增加/删减/查询 node，一定要把edge case考虑全面。
