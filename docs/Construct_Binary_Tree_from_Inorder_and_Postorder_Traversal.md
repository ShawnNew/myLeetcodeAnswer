## 106. Construct Binary Tree from Inorder and Postorder Traversal

Given inorder and postorder traversal of a tree, construct the binary tree.

**Note:**
You may assume that duplicates do not exist in the tree.

For example, given

```
inorder = [9,3,15,20,7]
postorder = [9,15,7,20,3]
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
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        return helper(inorder, postorder, postorder.length - 1, 0, inorder.length-1);
    }
    
    public TreeNode helper(int[] inorder, int[] postorder, int parentIndex, int inStart, int inEnd) {
        if (inStart > inEnd) return null;
        TreeNode root = new TreeNode(postorder[parentIndex]);
        int index = 0;
        for (int i = 0; i < inorder.length; i++) {
            if (root.val == inorder[i]) index = i;
        }
        
        // sub-left tree
        root.left = helper(inorder, postorder, parentIndex - (inEnd - index) - 1, inStart, index - 1);
        // sub-right tree
        root.right = helper(inorder, postorder, parentIndex - 1, index + 1, inEnd);
        return root;
    }
}
```

### 解题思路：
* 后续遍历从后往前第一个元素为root结点；
* 在中序遍历中找到root结点，就可以将元素分为左右子树；
* 左右子树分别递归即可；
* base case是中序遍历的开始指针超过结束指针，返回空结点；
* 当前的parent结点是后续遍历的最后一个元素；
* 左子树的根节点在后序遍历中为父亲结点的位置减去右子树的长度；
* 右子树的跟几点在后序遍历中为父亲结点的前一位置。