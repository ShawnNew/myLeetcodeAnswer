## 98. Validate Binary Search Tree

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

* The left subtree of a node contains only nodes with keys less than the node's key.
* The right subtree of a node contains only nodes with keys greater than the node's key.
* Both the left and right subtrees must also be binary search trees.

**Example 1:**

```
    2
   / \
  1   3
Binary tree [2,1,3], return true.
```

**Example 2:**

```
    1
   / \
  2   3
```
Binary tree [1,2,3], return false.

### Code

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
    public boolean isValidBST(TreeNode root) {
        if (root == null) return true;
        Stack<TreeNode> s = new Stack<TreeNode>();
        TreeNode pre = null;
        
        while (root != null || !s.isEmpty()) {
            while (root != null) {  //将所有的根结点压入栈
                s.push(root);
                root = root.left;
            } 
            root = s.pop();  //取出根结点
            if (pre != null && pre.val >= root.val) return false;
            pre = root;      //更新pre结点
            root = root.right; 
        }
        return true;
    }
}
```

### 解题思路

* 使用树的inOrderTraverse（中序遍历），使用pre结点记录前一结点；
* 依次访问左结点，根节点，右结点，BST的规则必须满足前一结点小于当前结点；
* 所以在遍历过程中，出现```pre.val >= root.val```则返回false。