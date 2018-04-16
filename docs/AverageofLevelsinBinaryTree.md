## 637. Average of Levels in Binary Tree

Given a non-empty binary tree, return the average value of the nodes on each level in the form of an array.

**Example 1:**

```
Input:
    3
   / \
  9  20
    /  \
   15   7

Output: [3, 14.5, 11]
Explanation:
The average value of nodes on level 0 is 3,  on level 1 is 14.5, and on level 2 is 11. Hence return [3, 14.5, 11].
```

**Note:**
The range of node's value is in the range of 32-bit signed integer.

### Code

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def averageOfLevels(self, root):
        """
        :type root: TreeNode
        :rtype: List[float]
        """
        res = [] #result
        if not root:
            return res
        
        queue = []  #每一层的队列
        queue.append(root)
        
        
        while queue:
            sum = 0
            n = len(queue)
            for i in range(n):  # 每一层的结点个数
                node = queue.pop()
                sum += float(node.val)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            
            res.append(sum / n)
            
        return res
```

### 解题思路

思路可以参考数的层次遍历