## 110. Balanced Binary Tree

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

> a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

**Example 1:**

Given the following tree [3,9,20,null,null,15,7]:

```
    3
   / \
  9  20
    /  \
   15   7
```

Return true.

**Example 2:**

Given the following tree [1,2,2,3,3,null,null,4,4]:

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```
Return false.

### Code:

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isBalanced(TreeNode root) {
        if (root == null) return true;
        
        int left = helper(root.left);
        int right = helper(root.right);
        
        return Math.abs(left - right) <= 1 && isBalanced(root.left) && isBalanced(root.right);
    }
    
    public int helper(TreeNode node) {
        if (node == null) return 0;
        return Math.max(helper(node.left), helper(node.right)) + 1;
        
    }
}
```

### 解题思路
* 使用辅助函数helper递归计算树的深度；
* left和right差别不大于1且左右子树分别平衡，则返回真；
* 返回值：```Math.abs(left - right) <= 1 && isBalanced(root.left) && isBalanced(root.right);```


### 一个递归

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isBalanced(TreeNode root) {
        return helper(root) != -1;
    }
    
    public int helper(TreeNode node) {
        if (node == null) return 0;
        int left = helper(node.left);
        int right = helper(node.right);
        if (left == -1 || right == -1 || Math.abs(left - right) > 1) return -1;
        return Math.max(left, right) + 1;
    }
}
``` 

* 在递归使用helper计算树的深度的时候，如果树不平衡，则返回-1；
* 如果树平衡，则返回树的深度。