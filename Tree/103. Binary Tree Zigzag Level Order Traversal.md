## 103. Binary Tree Zigzag Level Order Traversal

Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:
Given binary tree [3,9,20,null,null,15,7],

```
    3
   / \
  9  20
    /  \
   15   7
```
return its zigzag level order traversal as:

```
[
  [3],
  [20,9],
  [15,7]
]
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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        Stack<TreeNode> s1 = new Stack<TreeNode>();
        Stack<TreeNode> s2 = new Stack<TreeNode>();
        s2.push(root);
        while (!s1.isEmpty() || !s2.isEmpty()) {
            if (s1.isEmpty()) {
                List<Integer> temp = new ArrayList<Integer>();
                while (!s2.isEmpty()) {
                    TreeNode node = s2.pop();
                    if (node != null) {  // 判断是否为空结点，如果是空结点则跳过
                        temp.add(node.val);
                        s1.push(node.left);
                        s1.push(node.right);
                    } else continue;
                }
                if (temp.size() != 0) result.add(temp);
            }
            
            if (s2.isEmpty()) {
                List<Integer> temp = new ArrayList<Integer>();
                while (!s1.isEmpty()) {
                    TreeNode node = s1.pop();
                    if (node != null) {
                        temp.add(node.val);
                        s2.push(node.right);
                        s2.push(node.left);
                    } else continue; 
                    
                }
                if (temp.size() != 0) result.add(temp);
            }
        }
        return result;
    }
}
```

### 解题思路
* 该题是一个BFS，将树的每一层元素压入栈，每一层遍历完再遍历下一层；
* 使用两个栈辅助存储元素，root结点压入s2，当遍历s2中元素向s1中入栈时，先存左结点，再存右结点；
* 当遍历s1中元素向s2中入栈时，先存右结点，再存左结点；
* 注意在遍历栈中元素时要判断结点是否为空结点，如果为空，则要跳过。