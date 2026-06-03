# 📝 LeetCode 学习日志 Day 13

<br>

## 110. 平衡二叉树
- 题目链接：[**LeetCode 110. Balanced Binary Tree**](https://leetcode.com/problems/balanced-binary-tree/)
- 关键词：**Recursion**  

<br>

## 💡 思路
这道题是通过recursion的方式。先写recursion method，如果左右高度差大于1，就return -1，不是的话就return当前高度，最后看这个recursion是不是return -1。

<br>

## 💻 代码实现
```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return getHeight(root) != -1;
    }

    public int getHeight(TreeNode root){
        if(root == null) return 0;
        int leftHeight = getHeight(root.left);
        if(leftHeight == -1) return -1;
        int rightHeight = getHeight(root.right);
        if(rightHeight == -1) return -1;

        if(Math.abs(leftHeight - rightHeight) > 1) return -1;
        return Math.max(leftHeight, rightHeight) + 1;
    }
}
```

```python
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        def getHeight(root):
            if not root:
                return 0
            leftHeight = getHeight(root.left)
            rightHeight = getHeight(root.right)
            if leftHeight == -1 or rightHeight == -1 or abs(leftHeight - rightHeight) > 1:
                return -1
            return max(leftHeight,rightHeight) + 1
        return getHeight(root) is not -1
```

<br>

## 257. 二叉树的所有路径
- 题目链接：[**LeetCode 257. Binary Tree Paths**](https://leetcode.com/problems/binary-tree-paths/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题也是采用了recursion的方法。主要用到StringBuilder来进行node的添加。如果node的左右child都是null，那就是到了叶子，就只要把node.val加进去就行。其他情况则加入node.val和->。


<br>

## 💻 代码实现
```java
class Solution {
    List<String> result = new ArrayList<>();
    public List<String> binaryTreePaths(TreeNode root) {
        makePath(root, "");
        return result;
    }

    public void makePath(TreeNode node, String s){
        if(node == null) return;
        if(node.left == null && node.right == null){
            result.add(new StringBuilder(s).append(node.val).toString());
            return;
        }
        String temp = new StringBuilder(s).append(node.val).append("->").toString();
        makePath(node.left, temp);
        makePath(node.right, temp);
    }
}
```

```python
class Solution:
    def binaryTreePaths(self, root: Optional[TreeNode]) -> List[str]:
        path = ''
        result = []
        if not root:
            return result
        self.traversal(root, path, result)
        return result
    
    def traversal(self, cur: TreeNode, path: str, result: List[str]) -> None:
        path += str(cur.val)
        if not cur.left and not cur.right:
            result.append(path)
        if cur.left:
            self.traversal(cur.left, path + '->', result)
        if cur.right:
            self.traversal(cur.right, path + '->', result)
```

<br>

## 404. 左叶子之和
- 题目链接：[**LeetCode 404. Sum of Left Leaves**](https://leetcode.com/problems/sum-of-left-leaves/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题采用了recursion的办法，变得简单灵巧。重点在于怎么判断他是左叶子，当这个father node有一个left child，然后这个child的左右两边都是null，则这个就是个左叶子。

<br>

## 💻 代码实现
```java
class Solution {
    public int sumOfLeftLeaves(TreeNode root) {
        if(root == null) return 0;
        if(root.left == null && root.right == null) return 0;
        int left = sumOfLeftLeaves(root.left);
        if(root.left != null && root.left.left == null && root.left.right == null) left = root.left.val;
        int right = sumOfLeftLeaves(root.right);
        int sum = left + right;
        return sum;
    }
}
```

```python
class Solution:
    def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        leftValue = 0
        if root.left and not root.left.left and not root.left.right:
            leftValue = root.left.val
        return leftValue + self.sumOfLeftLeaves(root.left) + self.sumOfLeftLeaves(root.right)
```

<br>

## 222. 完全二叉树的节点个数
- 题目链接：[**LeetCode 222. Count Complete Tree Nodes**](https://leetcode.com/problems/count-complete-tree-nodes/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题采用了recursion的办法，变得简单灵巧。这个是通用算完全二叉树/满二叉树的解法。只需要采用recursion把node数量相加return就行。

<br>

## 💻 代码实现
```java
class Solution {
    public int countNodes(TreeNode root) {
        if(root == null) {
            return 0;
        }
        return countNodes(root.left) + countNodes(root.right) + 1;
    }
}
```

```python
class Solution:
    def countNodes(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        return 1 + self.countNodes(root.left) + self.countNodes(root.right)
```

<br>

## 📝 今日心得
今天的题目重点采用了recursion的方法去写，慢慢能抓到recursion是怎么写的了。**重点就还是在以下三点：**

- **确定递归函数的参数和返回值**
- **确定终止条件**
- **确定单层递归的逻辑**
