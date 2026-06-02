# 📝 LeetCode 学习日志 Day 12

<br>

## 226. 翻转二叉树
- 题目链接：[**LeetCode 226. Invert Binary Tree**](https://leetcode.com/problems/invert-binary-tree/)
- 关键词：**Recursion**  

<br>

## 💡 思路
这道题比较的简单，但是也需要理解明白其中的意思。最直接的就是用recursion的办法。以下的方法是采用了前序遍历的方法（中左右），先swap中间的node，再进行到他们的children。

<br>

## 💻 代码实现
```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root == null) return root;
        swap(root);
        invertTree(root.left);
        invertTree(root.right);
        return root;
    }

    public void swap(TreeNode root){
        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
    }
}
```

<br>

## 101. 对称二叉树
- 题目链接：[**LeetCode 101. Symmetric Tree**](https://leetcode.com/problems/symmetric-tree/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题也是采用了recursion的方法。主要分析有以下几种情况：
 - 左为空，右不为空 -> false
 - 左不为空，右为空 -> false
 - 左为空，右为空 -> true
 - 左不为空，右不为空，但左右值不同 -> false

这样就可以继续这个recursion，看两边外侧是否相同，内侧是否相同，将最终的结果return回去。


<br>

## 💻 代码实现
```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return compare(root.left, root.right);
    }

    private boolean compare(TreeNode left, TreeNode right){
        if(left != null && right == null) return false;
        else if(left == null && right != null) return false;
        else if(left == null && right == null) return true;
        else if(left.val != right.val) return false;
        else{
            boolean outside = compare(left.left, right.right);
            boolean inside = compare(left.right, right.left);
            return outside && inside;
        }
    }
}
```

<br>

## 104. 二叉树的最大深度
- 题目链接：[**LeetCode 104. Maximum Depth of Binary Tree**](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题采用了recursion的办法，变得简单灵巧。采用了后序遍历的方法，从叶子末尾开始算高度，直至根部。

<br>

## 💻 代码实现
```java
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null) return 0;
        int leftDepth = maxDepth(root.left);
        int rightDepth = maxDepth(root.right);
        return Math.max(leftDepth, rightDepth) + 1;
    }
}
```

<br>

## 111. 二叉树的最小深度
- 题目链接：[**LeetCode 111. Minimum Depth of Binary Tree**](https://leetcode.com/problems/minimum-depth-of-binary-tree/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题采用了recursion的办法，变得简单灵巧。看似跟最大深度一样，其实这里面有坑。要的是叶子到根的最短距离，叶子必须是左右两边都为null。所以如果一边有child另一边没有的话，就要return有node这一边的深度。

<br>

## 💻 代码实现
```java
class Solution {
    public int minDepth(TreeNode root) {
        if(root == null) return 0;
        int leftDepth = minDepth(root.left);
        int rightDepth = minDepth(root.right);
        if(root.left != null && root.right == null) return leftDepth + 1;
        if(root.right != null && root.left == null) return rightDepth + 1;
        return Math.min(leftDepth, rightDepth) + 1;
    }
}
```

<br>

## 📝 今日心得
今天的所有题目都是采用了recursion的方法。在这几道题里面，其实用recursion或者层序遍历的方式都可以实现，这两种方法都得熟练掌握。

今天也重点学习了写recursion的步骤：
 
- **确定递归函数的参数和返回值**
- **确定终止条件**
- **确定单层递归的逻辑**

虽然说recursion看起来不太好理解，但也还是能够掌握的，还需多加练习。