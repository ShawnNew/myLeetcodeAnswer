## 111. Minimum Depth of Binary Tree

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.


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
    public int minDepth(TreeNode root) {
        if(root == null) return 0;
        int left = minDepth(root.left);
        int right = minDepth(root.right);
        return (left == 0 || right == 0) ? left + right + 1: Math.min(left,right) + 1;
    }
}
```

### 解题思路
* 使用递归分别求出左右子树的最小深度；
* base case是当前结点为null；
* 递归式是：
	* 当前结点的左右子树非空：```Math.min(minDepth(root.left), minDepth(root.right)) + 1;```
	* 当前结点左右子树有一个为空：```minDepth(root.left) + minDepth(root.right) + 1;```
* 返回最小深度。