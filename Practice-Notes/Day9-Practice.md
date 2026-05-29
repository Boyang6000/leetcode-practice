# 📝 LeetCode 学习日志 Day 9

<br>

## 232.用栈实现队列
- 题目链接：[**LeetCode 232. Implement Queue Using Stack**](https://leetcode.com/problems/implement-queue-using-stacks/)
- 关键词：**Queue, Stack**  

<br>

## 💡 思路
这道题就是考察对Queue和Stack的理解程度。建立两个Stack，StackIn和StackOut，然后push的时候push到StackIn，pop和peek时先把stackIn里面的数字push到stackOut里面，这样先加入到stackIn的数字（在stack的末尾）就会变成stackOut的最上面，实现了FIFO

<br>

## 💻 代码实现
```java
class MyQueue {
    Stack<Integer> stackIn;
    Stack<Integer> stackOut;

    public MyQueue() {
        stackIn = new Stack<>();
        stackOut = new Stack<>();
    }
    
    public void push(int x) {
        stackIn.push(x);
    }
    
    public int pop() {
        dumpstackIn();
        return stackOut.pop();
    }
    
    public int peek() {
        dumpstackIn();
        return stackOut.peek();
    }
    
    public boolean empty() {
        return stackIn.isEmpty() && stackOut.isEmpty();
    }

    private void dumpstackIn(){
        if(!stackOut.isEmpty()) return;
        while(!stackIn.isEmpty()){
            stackOut.push(stackIn.pop());
        }
    }
}
```

```python
class MyQueue:

    def __init__(self):
        self.in_stack = []
        self.out_stack = []

    def push(self, x: int) -> None:
        self.in_stack.append(x)

    def pop(self) -> int:
        self.peek()
        return self.out_stack.pop()

    def peek(self) -> int:
        if not self.out_stack:
            while self.in_stack:
                self.out_stack.append(self.in_stack.pop())
        return self.out_stack[-1]

    def empty(self) -> bool:
        return not self.in_stack and not self.out_stack
```

<br>

## 225. 用队列实现栈
- 题目链接：[**LeetCode 225. Implement Stack Using Queues**](https://leetcode.com/problems/implement-stack-using-queues/)
- 关键词：**Deque, ArrayDeque, Stack**

<br>

## 💡 思路
这道题用Deque中的ArrayDeque来实现，因为ArrayDeque可以在首位和末尾进行push，pop，peek，比较方便

这里面的offer跟push相同，push失败的时候会throw execption，offer失败时会return false。

这里在push的时候就将里面元素的顺序反过来了，满足stack先进后出的原则

<br>

## 💻 代码实现
```java
class MyStack {
    private Deque<Integer> q = new ArrayDeque<>();

    public void push(int x) {
        q.offer(x);
        for (int i = 0; i < q.size() - 1; i++) {
            q.offer(q.poll());
        }
    }

    public int pop() {
        return q.poll();
    }

    public int top() {
        return q.peek();
    }

    public boolean empty() {
        return q.isEmpty();
    }
}
```

```python
class MyStack:

    def __init__(self):
        self.q = deque()

    def push(self, x: int) -> None:
        self.q.append(x)
        for i in range(len(self.q) - 1):
            self.q.append(self.q.popleft())

    def pop(self) -> int:
        return self.q.popleft()

    def top(self) -> int:
        return self.q[0]

    def empty(self) -> bool:
        return not self.q
```

<br>

## 20. 有效的括号
- 题目链接：[**LeetCode 20. Valid Parentheses**](https://leetcode.com/problems/valid-parentheses/description/)
- 关键词：**Deque, ArrayDeque**

<br>

## 💡 思路
这道题就是对于stack的运用，stack通常在括号匹配中使用，这里我们通过ArrayDeque来实现stack的功能。

当遇到一个左括号时，我们就把相对应的右括号加入到stack里面。

三种情况会return false：
 - 左括号多于右括号
 - 右括号多于左括号
 - 括号类型不匹配

<br>

## 💻 代码实现
```java
class Solution {
    public boolean isValid(String s) {
        Deque<Character> stack = new ArrayDeque<>();
        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            if (ch == '(') stack.push(')');
            else if (ch == '{') stack.push('}');
            else if (ch == '[') stack.push(']');
            else if (stack.isEmpty() || stack.peek() != ch) return false;
            else stack.pop();
        }
        return stack.isEmpty();
    }
}
```

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        for i in range(len(s)):
            char = s[i]
            if char == "(":
                stack.append(")")
            elif char == "[":
                stack.append("]")
            elif char == "{":
                stack.append("}")
            elif not stack or char != stack[-1]:
                return False
            else:
                stack.pop()
        return not stack  
```

<br>

## 1047. 删除字符串中的所有相邻重复项
- 题目链接：[**LeetCode 1047. Remove All Adjacent Duplicates in String**](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)
- 关键词：**ArrayDeque**

<br>

## 💡 思路
这道题也是一个stack的运用，这里用ArrayDeque来实现stack的功能。

先创建一个ArrayDeque，如果stack里面最后一位跟即将加入的字母一样，那么直接去除最后一位。如果不是前面这种情况则直接加入新的字母。最后将stack里面的字母转化为string。

<br>

## 💻 代码实现
```java
class Solution {
    public String removeDuplicates(String s) {
        Deque<Character> stack = new ArrayDeque<>();
        for(int i = 0; i < s.length(); i++){
            if(!stack.isEmpty() && stack.peekLast() == s.charAt(i)){
                stack.pollLast();
            }
            else{
                stack.addLast(s.charAt(i));
            }
        }
        
        StringBuilder sb = new StringBuilder();
        for (char c : stack) {
            sb.append(c);
            }
        return sb.toString();
    }
}
```

```python
class Solution:
    def removeDuplicates(self, s: str) -> str:
        stack = []
        for i in range(len(s)):
            char = s[i]
            if not stack or char != stack[-1]:
                stack.append(char)
            else:
                stack.pop()
        return ''.join(stack) 
```

<br>

## 📝 今日心得
对于stack和queue的实现还是不太熟悉和熟练。基本上用的最多的就是Deque来实现stack和queue，因为他可以在两端增加删除element，其中用的比较多的就是ArrayDeque，LinkedList用的少一些。可以多加练习和熟练每个类型里面可以使用的method。