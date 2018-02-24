## 94. Binary Tree Inorder Traversal

Given a binary tree, return the inorder traversal of its nodes' values.

For example:
Given binary tree [1,null,2,3],

```
  1
    \
     2
    /
   3
```

return [1,3,2].

**Note:** Recursive solution is trivial, could you do it iteratively?


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
    public List<Integer> inorderTraversal(TreeNode root) {
        LinkedList<TreeNode> stack = new LinkedList<>();
        List<Integer> result = new LinkedList<>();
        TreeNode pNode = root;
        while (pNode != null || !stack.isEmpty()) {
            if (pNode != null) {
                stack.push(pNode);  //将parent入栈
                pNode = pNode.left;  //当前结点置为左子树
            } else {    //当前结点为空，访问到叶子结点
                TreeNode node = stack.pop();      //parent出栈
                result.add(node.val);
                pNode = node.right;  //置为右子树
            }
        }
        return result;
    }
}
```

### 解题思路

* 二叉树的中序遍历，顺序为：leftNode --> parentNode --> rightNode
* 非递归的方法需要借助栈来存储parent结点，将当前结点置为左子树，直到找到叶子结点开始返回parent，并将当前结点置为右子树。
