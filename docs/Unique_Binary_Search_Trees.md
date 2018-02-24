## 96. Unique Binary Search Trees

Given n, how many structurally unique BST's (binary search trees) that store values 1...n?

For example,
Given n = 3, there are a total of 5 unique BST's.

```
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
   
```

### Code

```java
class Solution {
    public int numTrees(int n) {
        int[] BSTTable = new int[n+1];
        BSTTable[0] = 1;
        BSTTable[1] = 1;
        for (int level = 2; level <= n; level++) {
            for (int root = 1; root <= level; root++)
                BSTTable[level] += BSTTable[root-1] * BSTTable[level-root];  //root左边的所有结果乘root右边的所有结果
        }
        return BSTTable[n];
    }
}
```

### 解题思路

* 使用动态规划解题，BSTTable数组存储n个数时的BST总数；
* n=0和n=1时，都只有一种情况；
* 在1,...,n这n个数中，依次选取i作为root结点，对于每一种root，所形成的BST的数量等于root左子树的数目乘上root右子树的数目；
* 其中对于n个数，root作为根结点的情况，左子树的个数为BSTTable[root-1],右子树的个数为BSTTable[n-(root+1)+1]。