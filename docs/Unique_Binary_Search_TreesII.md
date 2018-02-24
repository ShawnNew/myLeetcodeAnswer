## 95. Unique Binary Search Trees II

Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1...n.

For example,
Given n = 3, your program should return all 5 unique BST's shown below.

```
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
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
    public List<TreeNode> generateTrees(int n) {
        if (n == 0) return new ArrayList<TreeNode>();
        return helper(1, n);
    }
    public List<TreeNode> helper(int start, int end) {
        List<TreeNode> result = new ArrayList<TreeNode>();
        if (start > end) {
            result.add(null);
            return result;
        }
        if (start == end) {
            result.add(new TreeNode(start));
            return result;
        }
        
        for (int i = start; i <= end; i++) {
            List<TreeNode> left = helper(start, i-1);  //分别得到左右子树的结点列表
            List<TreeNode> right = helper(i+1, end);
            for (TreeNode lNode : left) {
                for (TreeNode rNode : right) {
                    TreeNode node = new TreeNode(i);
                    node.left = lNode;
                    node.right = rNode;
                    result.add(node);
                }
            }
        }
        return result;
    }
}
```

### 解题思路

* 使用递归的思路，对于root结点，小于root的值都放在左子树，大于root的值都放在右子树；
* 递归的base case是```start>end```返回空，和```start==end```返回node=start；
* 递归式为```left = helper(start, i-1);```和```right = helper(i+1, end);```
* 返回值是满足条件的左子树或者右子树的列表；
* 最后将左右子树的列表依次加入到根节点root上。