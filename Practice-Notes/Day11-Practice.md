# 📝 LeetCode 学习日志 Day 11

<br>

## 144. 二叉树的前序遍历
- 题目链接：[**LeetCode 144. Binary Tree Preorder Traversal**](https://leetcode.com/problems/binary-tree-preorder-traversal/)
- 关键词：**Binary Tree, Preorder, Recursion, Iteration, Stack**  

<br>

## 💡 思路
首先，我们要知道**前序遍历**的顺序：**中左右**

**递归法**:
- 采用Recursion的方式，先写出一个recursion的method，然后在call这个method。这种方式是通过系统栈来实现的

**迭代法**：
- 这个是通过自己创建的stack来实现的。因为stack是后入先出，然后前序遍历的顺序是中左右，所以我们会先将中间node加入到结果里面，因为中是需要立即访问的，然后我们会先把右边加入到stack里面，再把左边加入到stack里面，确保左边node会先进行遍历。

**统一迭代法**：
- 使用统一迭代法是因为如果用普通的迭代法的话，中序遍历的逻辑跟前后序遍历的逻辑不一样，会相对麻烦一些。采用统一迭代法的话可以让三个逻辑统一。
- 统一迭代法的逻辑就是将node以倒序的形式加入到stack里面，在中node加入之后加入一个null node。这个null node表示这个node的所有children都已经访问完了，接下来可以加入这个node的值到result里了。这样保证了前中后序的逻辑是一样的。
<br>

## 💻 代码实现

### 递归法

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result =  new ArrayList<>();
        preorder(root, result);
        return result;
    }

    public void preorder(TreeNode root, List<Integer> result){
        if(root == null) return;
        result.add(root.val);
        preorder(root.left, result);
        preorder(root.right, result);
    }
}
```

```python
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res = []
        def dfs(node):
            if not node:
                return
            res.append(node.val)
            dfs(node.left)
            dfs(node.right)
        dfs(root)
        return res
```

### 迭代法

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        List<Integer> result = new ArrayList<>();
        if(root == null) return result;
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode node = stack.pop();
            result.add(node.val);
            if(node.right != null) stack.push(node.right);
            if(node.left != null) stack.push(node.left);
        }
        return result;
    }
}
```

### 统一迭代法

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        if(root != null) stack.push(root);
        while(!stack.isEmpty()){
            TreeNode node = stack.peek();
            if(node != null){
                stack.pop();
                if(node.right != null) stack.push(node.right);
                if(node.left != null) stack.push(node.left);
                stack.push(node);
                stack.push(null);
            }
            else{
                stack.pop();
                node = stack.pop();
                result.add(node.val);
            }
        }
        return result;
    }
}
```

<br>

## 145. 二叉树的后序遍历
- 题目链接：[**LeetCode 145. Binary Tree Postorder Traversal**](https://leetcode.com/problems/binary-tree-postorder-traversal/)
- 关键词：**Binary Tree, Preorder, Recursion, Iteration, Stack**

<br>

## 💡 思路
首先，我们要知道**后序遍历**的顺序：**左右中**

**递归法**:
- 采用Recursion的方式，先写出一个recursion的method，然后在call这个method。这种方式是通过系统栈来实现的

**迭代法**：
- 这个是通过自己创建的stack来实现的。因为stack是后入先出，然后后序遍历的顺序是左右中，所以我们会先将中间node加入到结果里面，因为中是需要立即访问的，然后我们会先把左边加入到stack里面，再把右边加入到stack里面，最后整个reverse，就得到了顺序左右中。

**统一迭代法**：
- 使用统一迭代法是因为如果用普通的迭代法的话，中序遍历的逻辑跟前后序遍历的逻辑不一样，会相对麻烦一些。采用统一迭代法的话可以让三个逻辑统一。
- 统一迭代法的逻辑就是将node以倒序的形式加入到stack里面，在中node加入之后加入一个null node。这个null node表示这个node的所有children都已经访问完了，接下来可以加入这个node的值到result里了。这样保证了前中后序的逻辑是一样的。

<br>

## 💻 代码实现

### 递归法

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        postorder(root, result);
        return result;
    }

    public void postorder(TreeNode root, List<Integer> result){
        if(root == null) return;
        postorder(root.left, result);
        postorder(root.right, result);
        result.add(root.val);
    }
}
```

```python
class Solution:
    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res = []
        def dfs(node):
            if not node:
                return
            dfs(node.left)
            dfs(node.right)
            res.append(node.val)
        
        dfs(root)
        return res
```

### 迭代法

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        List<Integer> result = new ArrayList<>();
        if(root == null) return result;
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode node = stack.pop();
            result.add(node.val);
            if(node.left != null) stack.push(node.left);
            if(node.right != null) stack.push(node.right);
        }
        Collections.reverse(result);
        return result;    
    }
}
```

### 统一迭代法

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        if(root != null) stack.push(root);
        while(!stack.isEmpty()){
            TreeNode node = stack.peek();
            if(node != null){
                stack.pop();
                stack.push(node);
                stack.push(null);
                if(node.right != null) stack.push(node.right);
                if(node.left != null) stack.push(node.left);
            }
            else{
                stack.pop();
                node = stack.pop();
                result.add(node.val);
            }
        }
        return result;
    }
}
```

<br>

## 94. 二叉树的中序遍历
- 题目链接：[**LeetCode 94. Binary Tree Inorder Traversal**](https://leetcode.com/problems/binary-tree-inorder-traversal/)
- 关键词：**Binary Tree, Preorder, Recursion, Iteration, Stack**

<br>

## 💡 思路
首先，我们要知道**中序遍历**的顺序：**左中右**

**递归法**:
- 采用Recursion的方式，先写出一个recursion的method，然后在call这个method。这种方式是通过系统栈来实现的

**迭代法**：
- 这个是通过自己创建的stack来实现的。=中序遍历的迭代法和前后序的不同，他是先将左边所有的node一个个加入到stack里面，然后再pop出来加入右边node。

**统一迭代法**：
- 使用统一迭代法是因为如果用普通的迭代法的话，中序遍历的逻辑跟前后序遍历的逻辑不一样，会相对麻烦一些。采用统一迭代法的话可以让三个逻辑统一。
- 统一迭代法的逻辑就是将node以倒序的形式加入到stack里面，在中node加入之后加入一个null node。这个null node表示这个node的所有children都已经访问完了，接下来可以加入这个node的值到result里了。这样保证了前中后序的逻辑是一样的。

<br>

## 💻 代码实现

### 递归法

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        inorder(root, result);
        return result;
    }

    public void inorder(TreeNode root, List<Integer> result){
        if(root == null) return;
        inorder(root.left, result);
        result.add(root.val);
        inorder(root.right, result);
    }
}
```

```python
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res = []
        def dfs(node):
            if not node:
                return
            dfs(node.left)
            res.append(node.val)
            dfs(node.right)
        
        dfs(root)
        return res
```

### 迭代法

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        while(cur != null || !stack.isEmpty()){
            if(cur != null){
                stack.push(cur);
                cur = cur.left;
            }
            else{
                cur = stack.pop();
                result.add(cur.val);
                cur = cur.right;
            }
        }
        return result;
    }
}
```

### 统一迭代法

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        if(root != null) stack.push(root);
        while(!stack.isEmpty()){
            TreeNode node = stack.peek();
            if(node != null){
                stack.pop();
                if(node.right != null) stack.push(node.right);
                stack.push(node);
                stack.push(null);
                if(node.left != null) stack.push(node.left);
            }
            else{
                stack.pop();
                node = stack.pop();
                result.add(node.val);
            }
        }
        return result;
    }
}
```

<br>

## 102. 二叉树的层序遍历
- 题目链接：[**LeetCode 102. Binary Tree Level Order Traversal**](https://leetcode.com/problems/binary-tree-level-order-traversal/)
- 关键词：**Binary Tree, Queue, BFS**

<br>

## 💡 思路
这道题和解法就是整个层序遍历的模板，使用queue来进行层序遍历，也就是广度优先遍历BFS。

先创建一个Queue，然后将root加入进去，通过queue的size来确定每一层里面有几个node，将这几个node处理完之后把他们的children都加入到这个queue里面直至处理完。

<br>

## 💻 代码实现


```java
class Solution {
    List<List<Integer>> resList = new ArrayList<List<Integer>>();
    public List<List<Integer>> levelOrder(TreeNode root) {
        BFS(root);
        return resList;
    }

    public void BFS(TreeNode node){
        Queue<TreeNode> queue = new LinkedList<>();
        if(node == null) return;
        queue.offer(node);

        while(!queue.isEmpty()){
            List<Integer> item = new ArrayList<>();
            int len = queue.size();
            while(len > 0){
                TreeNode tempNode = queue.poll();
                item.add(tempNode.val);

                if(tempNode.left != null) queue.offer(tempNode.left);
                if(tempNode.right != null) queue.offer(tempNode.right);

                len--;
            }
            resList.add(item);
        }
    }
}
```

```python
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        
        res = []

        def traverse(node, level):
            if not node:
                return
            if len(res) == level:
                res.append([])
            res[level].append(node.val)
            traverse(node.left, level + 1)
            traverse(node.right, level + 1)
            
        traverse(root, 0)
        return res
```

## 107. 二叉树的层序遍历 II
- 题目链接：[**LeetCode 107. Binary Tree Level Order Traversal II**](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/)
- 关键词：**Binary Tree, Queue, BFS**

<br>

## 💡 思路
这道题的思路跟102一样，用queue实现BFS，只要在最后把list反转就可以了。

<br>

## 💻 代码实现


```java
class Solution {
    List<List<Integer>> resList = new ArrayList<List<Integer>>();
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        DFS(root);
        Collections.reverse(resList);
        return resList;
    }

    public void DFS(TreeNode node){
        Queue<TreeNode> queue = new LinkedList<>();
        if(node == null) return;
        queue.offer(node);

        while(!queue.isEmpty()){
            List<Integer> item = new ArrayList<>();
            int len = queue.size();
            while(len > 0){
                TreeNode temp = queue.poll();
                item.add(temp.val);
                if(temp.left != null) queue.offer(temp.left);
                if(temp.right != null) queue.offer(temp.right);
                len--;
            }
            resList.add(item);
        }
    }
}
```

```python
class Solution:
    def levelOrderBottom(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []

        queue = collections.deque([root])
        result = []
        while queue:
            level = []
            for i in range(len(queue)):
                cur = queue.popleft()
                level.append(cur.val)
                if cur.left:
                    queue.append(cur.left)
                if cur.right:
                    queue.append(cur.right)
            result.append(level)
        return result[::-1]
```

## 199. 二叉树的右视图
- 题目链接：[**LeetCode 199. Binary Tree Right Side View**](https://leetcode.com/problems/binary-tree-right-side-view/)
- 关键词：**Binary Tree, Queue, BFS**

<br>

## 💡 思路
这道题的思路也是从102上做延伸，用Queue做BFS，先得出每一层的size，然后再用for loop到最后一个node，把最后一个node加入到list里面。

<br>

## 💻 代码实现


```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        if(root == null) return list;
        queue.offer(root);
        while(!queue.isEmpty()){
            int levelSize = queue.size();
            for(int i = 0; i < levelSize; i++){
                TreeNode temp = queue.poll();
                if(temp.left != null) queue.offer(temp.left);
                if(temp.right != null) queue.offer(temp.right);
                if(i == levelSize - 1) list.add(temp.val);
            }
        }
        return list;
    }
}
```

```python
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []
        res = []
        queue = collections.deque([root])
        while queue:
            level = len(queue)
            for i in range(level):
                node = queue.popleft()
                if i == level - 1:
                    res.append(node.val)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        
        return res
```

## 637. 二叉树的层平均值
- 题目链接：[**LeetCode 637. Average of Levels in Binary Tree**](https://leetcode.com/problems/average-of-levels-in-binary-tree/)
- 关键词：**Binary Tree, Queue, BFS**

<br>

## 💡 思路
这道题的思路也是从102上做延伸，用Queue做BFS，先得出每一层的size，然后把一层里node的value加在一起做average。

<br>

## 💻 代码实现


```java
class Solution {
    public List<Double> averageOfLevels(TreeNode root) {
        List<Double> list = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        if(root == null) return list;
        queue.offer(root);
        while(!queue.isEmpty()){
            int levelSize = queue.size();
            Double sum = 0.0;
            for(int i = 0; i < levelSize; i++){
                TreeNode temp = queue.poll();
                if(temp.left != null) queue.offer(temp.left);
                if(temp.right != null) queue.offer(temp.right);
                sum += temp.val;
            }
            list.add(sum / levelSize);
        }
        return list;
    }
}
```

```python
class Solution:
    def averageOfLevels(self, root: Optional[TreeNode]) -> List[float]:
        if not root:
            return [0]
        res = []
        queue = collections.deque([root])
        while queue:
            level = len(queue)
            total = 0
            for i in range(level):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
                total += node.val
            res.append(total / level)
        return res
```

## 429. N叉树的层序遍历
- 题目链接：[**LeetCode 429. N-ary Tree Level Order Traversal**](https://leetcode.com/problems/n-ary-tree-level-order-traversal/)
- 关键词：**Tree, Queue, BFS**

<br>

## 💡 思路
这道题的思路也是从102上做延伸，用Queue做BFS，先得出每一层的size，然后把每一个node所有的children都加入到queue里面去。

<br>

## 💻 代码实现


```java
class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> resList = new ArrayList<>();
        Queue<Node> queue = new LinkedList<>();
        if(root == null) return resList;
        queue.offer(root);
        while(!queue.isEmpty()){
            int levelSize = queue.size();
            List<Integer> item = new ArrayList<>();
            for(int i = 0; i < levelSize; i++){
                Node temp = queue.poll();
                item.add(temp.val);
                List<Node> children = temp.children;
                if (children == null || children.size() == 0) {
                    continue;
                }
                for(Node child: temp.children){
                    if(child != null) queue.offer(child);
                }
            }
            resList.add(item);
        }
        return resList;
    }
}
```

## 515. 在每个树行中找最大值
- 题目链接：[**LeetCode 515. Find Largest Value in Each Tree Row**](https://leetcode.com/problems/find-largest-value-in-each-tree-row/)
- 关键词：**Binary Tree, Queue, BFS**

<br>

## 💡 思路
这道题的思路也是从102上做延伸，用Queue做BFS，在每一层的node里面找最大值。

<br>

## 💻 代码实现


```java
class Solution {
    public List<Integer> largestValues(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        if(root == null) return list;
        queue.offer(root);
        while(!queue.isEmpty()){
            int max = Integer.MIN_VALUE;
            int levelSize = queue.size();
            for(int i = 0; i < levelSize; i++){
                TreeNode temp = queue.poll();
                if(temp.val > max) max = temp.val;
                if(temp.left != null) queue.offer(temp.left);
                if(temp.right != null) queue.offer(temp.right);
            }
            list.add(max);
        }
        return list;
    }
}
```

## 116. 填充每个节点的下一个右侧节点指针
- 题目链接：[**LeetCode 116. Populating Next Right Pointers in Each Node**](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)
- 关键词：**Binary Tree, Queue, BFS, Two Pointers**

<br>

## 💡 思路
这道题的思路也是从102上做延伸，用Queue做BFS，然后用双指针给同一层的每个node连接在一起。

<br>

## 💻 代码实现


```java
class Solution {
    public Node connect(Node root) {
        Queue<Node> queue = new LinkedList<>();
        if(root == null) return root;
        queue.offer(root);
        while(!queue.isEmpty()){
            int levelSize = queue.size();
            Node cur = queue.poll();
            if(cur.left != null) queue.offer(cur.left);
            if(cur.right != null) queue.offer(cur.right);
            for(int i = 1; i < levelSize; i++){
                Node next = queue.poll();
                if(next.left != null) queue.offer(next.left);
                if(next.right != null) queue.offer(next.right);
                cur.next = next;
                cur = next;
            }
        }
        return root;
    }
}
```

## 117. 填充每个节点的下一个右侧节点指针II
- 题目链接：[**LeetCode 117. Populating Next Right Pointers in Each Node II**](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)
- 关键词：**Binary Tree, Queue, BFS, Two Pointers**

<br>

## 💡 思路
同116。

<br>

## 💻 代码实现


```java
class Solution {
    public Node connect(Node root) {
        Queue<Node> queue = new LinkedList<>();
        if(root == null) return root;
        queue.offer(root);
        while(!queue.isEmpty()){
            int levelSize = queue.size();
            Node cur = queue.poll();
            if(cur.left != null) queue.offer(cur.left);
            if(cur.right != null) queue.offer(cur.right);
            for(int i = 1; i < levelSize; i++){
                Node next = queue.poll();
                if(next.left != null) queue.offer(next.left);
                if(next.right != null) queue.offer(next.right);
                cur.next = next;
                cur = next;
            }
        }
        return root;
    }
}
```

## 104. 二叉树的最大深度
- 题目链接：[**LeetCode 104. Maximum Depth of Binary Tree**](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- 关键词：**Binary Tree, Queue, BFS**

<br>

## 💡 思路
这道题的思路也是从102上做延伸，从层序遍历上进行计算最大深度。

<br>

## 💻 代码实现


```java
class Solution {
    public int maxDepth(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        if(root != null) queue.offer(root);
        int depth = 0;
        while(!queue.isEmpty()){
            int len = queue.size();
            while(len > 0){
                 TreeNode temp = queue.poll();
                if(temp.left != null) queue.offer(temp.left);
                if(temp.right != null) queue.offer(temp.right);
                len--;
            }
            depth++;
        }
        return depth;
    }
}
```

## 111. 二叉树的最小深度
- 题目链接：[**LeetCode 111. Minimum Depth of Binary Tree**](https://leetcode.com/problems/minimum-depth-of-binary-tree/)
- 关键词：**Binary Tree, Queue, BFS**

<br>

## 💡 思路
这道题的思路也是从102上做延伸，从层序遍历上进行计算最小深度，当node没有左右child的时候，这一层就是最小深度。

<br>

## 💻 代码实现


```java
class Solution {
    public int minDepth(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        if(root != null) queue.offer(root);
        int depth = 0;
        while(!queue.isEmpty()){
            depth++;
            int len = queue.size();
            while(len > 0){
                 TreeNode temp = queue.poll();
                if(temp.left != null) queue.offer(temp.left);
                if(temp.right != null) queue.offer(temp.right);
                if(temp.left == null && temp.right == null) return depth;
                len--;
            }
        }
        return depth;
    }
}
```

## 📝 今日心得
今天的题目非常多，但是总体写法是一致的，只需要做小的修改就行。

总结一下二叉树遍历有**三种：前序遍历：中左右，中序遍历：左中右，后序遍历：左右中**。编写这三种遍历的方法也有**三种：递归法，迭代法，统一迭代法**。

其中，**统一迭代法**用的最多，这是采用了queue来进行层序遍历。后面的这十道题目都是通过层序遍历的方式写出来的。总体来说对于二叉树的练习非常的到位，不至于手足无措。