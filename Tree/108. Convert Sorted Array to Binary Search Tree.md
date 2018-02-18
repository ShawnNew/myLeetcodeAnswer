## 108. Convert Sorted Array to Binary Search Tree

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.


**Example:**

```
Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
 
```

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
public class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        return helper(nums, 0, nums.length-1);
    }
    
    public TreeNode helper(int[] nums, int start, int end) {
        if (start > end) return null;
        
        int midIndex = (start + end) >>> 1;
        TreeNode root = new TreeNode(nums[midIndex]);
        root.left = helper(nums, start, midIndex-1);
        root.right = helper(nums, midIndex+1, end);
        return root;
    }
}
```

### 解题思路

* 使用递归的解法，数组中的中间位置的元素作为根结点，根结点的左边和右边的元素分别划分为左子树和右子树，分别递归求解；
* base case是start>end，返回null；
* 递归式是当前结点的左右子树分别递归；
* 返回根结点。