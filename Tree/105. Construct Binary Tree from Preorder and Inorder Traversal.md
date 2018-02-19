## 105. Construct Binary Tree from Preorder and Inorder Traversal

Given preorder and inorder traversal of a tree, construct the binary tree.

**Note:**
You may assume that duplicates do not exist in the tree.

For example, given

```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
```
Return the following binary tree:

```
    3
   / \
  9  20
    /  \
   15   7
```

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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        return helper(0, 0, inorder.length - 1, preorder, inorder);
    }

    public TreeNode helper(int preStart, int inStart, int inEnd, int[] preorder, int[] inorder) {
        if (inStart > inEnd) {
            return null;
        }
        TreeNode root = new TreeNode(preorder[preStart]);
        int inIndex = 0; // Index of current root in inorder
        for (int i = inStart; i <= inEnd; i++) {
            if (inorder[i] == root.val) {
                inIndex = i;
            }
        }
        root.left = helper(preStart + 1, inStart, inIndex - 1, preorder, inorder);
        root.right = helper(preStart + inIndex - inStart + 1, inIndex + 1, inEnd, preorder, inorder);
        return root;
    }
}
```

### 解题思路
* 使用递归；
* 前序遍历中的第一个元素即为当前根节点，在中序遍历中找到根结点的位置，根节点的左边的元素都划分为左子树，根节点的右边的元素都划分为右子树；
* 然后分别递归构造左子树和右子树；
* base case是中序遍历的两指针越界；
* 递归式是，root结点的左子树：```root.left = helper(preStart+1, inStart, inIndex-1, preorder, inorder);```；
* 右子树：```root.right = helper(preStart+inIndex-inStart+1, inIndex+1, inEnd, preorder, inorder);```；
* 返回root结点。
